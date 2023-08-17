<template>
  <div class="chatbox">
    <div class="chatbox-content">
      <div class="messages" ref="messagesContainer">
        <transition name="typing" mode="out-in">
          <div>
            <div
              class="chat-container"
              v-for="(message, index) in messages"
              :key="index"
              :class="[
                message.type === 'user' ? 'user-message' : 'master-message',
              ]"
            >
              <img
                v-if="message.type === 'master'"
                :src="message.image"
                :alt="message.author"
                class="message-avatar"
              />

              <img
                v-else
                src="../assets/user.jpg"
                alt="User"
                class="message-avatar"
              />
              <div class="pre-wrap">{{ message.text }}</div>
            </div>
          </div>
        </transition>
      </div>
      <div class="spinner" v-if="loading">
        <img src="../assets/dustbin.png" />
      </div>
    </div>
    <form @submit.prevent="sendMessage">
      <input
        type="text"
        class="question-input"
        v-model="inputMessage"
        @input="validateInput"
        @keyup.enter="
          sendMessage();
          scrollToBottom();
        "
        placeholder="How do I find peace in the middle of chaos ?"
        ref="questionInput"
        v-on:input="validateInput"
        v-on:focus="validateInput"
      />
      <ion-button @click="sendMessage">
        <ion-icon :icon="paperPlaneOutline"></ion-icon>
      </ion-button>
    </form>
    <div v-show="messages.length > 0" class="clear-chat-button">
      <ion-button class="ion-no-padding" @click="clearChat">
      <ion-icon :icon="trashOutline"></ion-icon>
    </ion-button>
    </div>
    <ion-button class="send-button" @click="sendMessage">
      <ion-icon :icon="paperPlaneOutline"></ion-icon>
    </ion-button>
  </div>
</template>

<script>
import {
  IonButton,
  IonIcon,
  IonMenu,
  IonBackButton,
  toastController,
} from "@ionic/vue";
import { paperPlaneOutline, trashOutline } from "ionicons/icons";
import user from "../assets/user.jpeg";
import axios from "axios";
export default {
  name: "AppChatbox",
  props: {
    selectedMasters: {
      type: Array,
      default: () => [],
    },
    selectedMastersCount: {
      type: Number,
      required: true,
    },
  },
  components: {
    IonButton,
    IonIcon,
    IonMenu,
    IonBackButton,
  },
  data() {
    return {
      inputMessage: "",
      messages: [],
      typingMessage: "",
      userAvatar: user,
      loading: false,
      conversationHistory: [],
    };
  },
  methods: {
    clearChat() {
      this.messages = [];
      this.conversationHistory = [];
    },
    typeMessage(message) {
      let index = 0;
      const interval = setInterval(() => {
        if (index < message.length) {
          this.typingMessage += message[index];
          index++;
        } else {
          clearInterval(interval);
        }
      }, 100); // Adjust the typing speed by changing this value (milliseconds)
    },

    async getGptResponse(prompt, master) {
      console.log("Getting GPT response for prompt:", prompt);
      // Use the environment variable

      const apiKey = import.meta.env.VITE_APP_OPENAI_API_KEY;
      console.log(apiKey);
      const apiEndpoint = "https://api.openai.com/v1/chat/completions";
      const headers = {
        "Content-Type": "application/json",
        Authorization: `Bearer ${apiKey}`,
      };

      const data = {
        model: "gpt-3.5-turbo",
        messages: [
          ...this.conversationHistory, // Include the existing conversation history
          { role: "system", content: master.prompt },
          { role: "user", content: `Q: ${prompt}\n` },
        ],
      };

      try {
        console.log("Making API call with data:", data);
        const response = await axios.post(apiEndpoint, data, { headers });
        console.log(
          "GPT response:",
          response.data.choices[0].message.content.trim()
        );

        // Save the assistant's response to the conversation history
        this.conversationHistory.push({
          role: "assistant",
          content: response.data.choices[0].message.content.trim(),
        });

        return response.data.choices[0].message.content.trim();
      } catch (error) {
        console.error("Error calling ChatGPT API:", error);
        return "Sorry, I am unable to provide an answer at the moment.";
      } finally {
        this.scrollToBottom();
      }
    },

    scrollToBottom() {
      const element = document.getElementsByClassName("messages")[0];
      
      element.scrollTop = element.scrollHeight;
      
    },

    async sendMessage() {
      if (!this.selectedMastersCount) {
        const toast = await toastController.create({
          message: "Select at least one master to continue!",
          duration: 3000,
          position: "top",
          translucent: true,
          cssClass: "toast",
        });

        await toast.present();
        return;
      }
      if (!this.inputMessage) {
        return;
      }

      // if (!this.inputMessage || !this.selectedMasters.length) return;

      const userMessage = this.inputMessage;
      const userAvatar =
        "https://secure.gravatar.com/avatar/84e1cab23663f968345fafb812c73a85?s=50&d=mm&r=g";

      this.messages.push({
        authorImage: userAvatar,
        text: userMessage,
        type: "user",
      });
      this.inputMessage = "";
      this.loading = true;

      // Save the user's message to the conversation history
      this.conversationHistory.push({
        role: "user",
        content: `Q: ${userMessage}\n`,
      });

      for (const master of this.selectedMasters) {
        // Call the ChatGPT API and get response
        const gptResponse = await this.getGptResponse(userMessage, master);
        const masterResponse = {
          author: master.name,
          image: master.image,
          text: gptResponse,
          type: "master",
        };
        this.messages.push(masterResponse);
        this.scrollToBottom();
      }

      this.loading = false; // Add this line
    },
  },
  watch: {
    messages: {
      handler(after, before) {
        this.scrollToBottom();
      },
      deep: true,
    },

    selectedMasters: {
      immediate: true,
      handler(selectedMasters) {
        this.showHover = selectedMasters.length === 0;
      },
    },
  },
  mounted() {
    // Focus the input when the component is mounted
    this.$refs.questionInput.focus();
  },
  setup() {
    return {
      paperPlaneOutline,
      trashOutline
    };
  },
};
</script>

<style scoped>
ion-button {
  --background: white;
  border: none;
  --box-shadow: none;
  border-radius: 100%;
  padding: 0;
}
.send-button ion-icon {
  color: rgb(48, 48, 48);
}
.send-button {
  position: fixed;
  bottom: 5.5%;
  right: 3%;
  z-index: 1000000;
  --background: transparent;
}

button.button-native {
  padding: 0 !important;
}

.question-input {
  background-color: #fff;
  width: 95%;
  position: fixed;
  bottom: 5%;
  left: 2.5%;
  border: none;
  border-radius: 50px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding: 15px;
  outline: none;
}
.question-input:focus {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.clear-chat-button {
  position: fixed;
  top: 10%;
  right: 10px;
}

.clear-chat-button ion-icon {
  color: #f07812;
  font-size: 22px;
}
.chat-container {
  display: flex;
  margin: 6px 2%;
  line-height: 2.5vh;
}

.user-message {
  justify-content: end;
  flex-direction: row-reverse;
}

.user-message .message-avatar {
  margin-left: 10px;
}
.master-message .message-avatar {
  margin-right: 10px;
}

.message-avatar {
  height: 35px;
  border-radius: 100%;
  margin-top: 7px;
}

.pre-wrap {
  text-align: justify;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 20px;
  padding: 15px;
  background-color: #fff;
  max-width: 70%;
}

.messages {
  overflow-y: scroll;
}
.spinner {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;
}

@media (max-width: 767px) {
  .message-avatar {
    height: 30px;
    margin-top: 10px;
  }
  input::placeholder {
    font-size: 0.8rem;
  }
  .chat-container {
    margin: 6px 3%;
    font-size: 0.8rem;
  }
  .messages {
    overflow-y: scroll;
  }
}
@media (max-width: 300px) {
  input::placeholder {
    font-size: 0.6rem;
  }
}
</style>
