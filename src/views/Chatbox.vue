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
              <div
                class="pre-wrap"
                :class="{ 'pre-wrap-master': message.type === 'master' }"
              >
                {{ message.text }}

                <div v-if="message.type === 'master'" class="thumbs">
                  <button class="thumbButt" @click="vote(true, message.author)">
                    👍
                  </button>
                  <button
                    class="thumbButt"
                    @click="vote(false, message.author)"
                  >
                    👎
                  </button>
                  <button class="thumbButt" @click="copyMessage(message.text)">
                    📑 Copy
                  </button>
                </div>
              </div>
           </div>
          </div>
        </transition>
      </div>
      <div class="spinner" v-if="loading">
        <img style="width: 100px" src="../assets/new.gif" />
      </div>
    </div>
    <input
      type="text"
      class="question-input"
      v-model="inputMessage"
      @keyup.enter="
        sendMessage();
        scrollToBottom();
      "
      placeholder="How do I find peace in the middle of chaos ?"
      ref="questionInput"
    />
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
      MasterAndPromptsArr: [],
    };
  },
  methods: {
    clearChat() {
      this.messages = [];
      this.conversationHistory = [];
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

      //in this Arr we push master name and prompts
      this.MasterAndPromptsArr.push({
        name: master.name,
        prompt: master.prompt,
      });

      const data = {
        model: "gpt-3.5-turbo",
        messages: [
          ...this.conversationHistory, // Include the existing conversation history
          { role: "system", content: master.prompt },
          { role: "user", content: `${prompt}` },
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
        content: `${userMessage}`,
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

      // =======================================================
      const CH = this.conversationHistory;
      console.log({ CH });

      const QN = CH[0].content;

      const loggs1 = this.MasterAndPromptsArr.map((ele) => {
        return {
          Master: ele.name,
          Prompt: ele.prompt,
        };
      });

      const loggs2 = CH.slice(1).map((item) => {
        return {
          Question: QN,
          Answer: item.content,
        };
      });

      const combinedLoggs = loggs2.map((item, index) => {
        return {
          Master: loggs1[index].Master,
          Prompt: loggs1[index].Prompt, // Use the corresponding Master from loggs1
          ...item, // Spread the properties from loggs2
        };
      });

      // Create the obj object with the combinedLoggs array
      const obj = {
        loggs: combinedLoggs,
      };

      try {
        const LoggingsResponse = await axios.post(
          `https://agile-smock-worm.cyclic.app/loggings/post`,
          obj
        );
        console.log(LoggingsResponse.data.msg);
        this.conversationHistory = [];
        this.MasterAndPromptsArr = [];
      } catch (error) {
        console.error("Error sending POST request:", error);
      }
    },

    async vote(isUpvote, masterName) {
      // Find the master's message based on the master's name
      const message = this.messages.find((msg) => msg.author === masterName);

      if (!message) {
        console.error(`Master ${masterName}'s answer not found.`);
        return;
      }

      // Extract relevant data
      const masterMessage = message.text;

      // Create the object to send in the POST request
      const voteData = {
        answer: masterMessage,
        master: masterName,
        vote: isUpvote, // true for "👍", false for "👎"
      };

      try {
        const response = await axios.post(
          "http://localhost:3000/thumbvote/post",
          voteData
        );
        if (response.status === 200) {
          this.thankYouMessage = true;
          alert(
            `Vote ${
              isUpvote ? "👍" : "👎"
            } sent successfully for ${masterName}'s answer!`
          );
        } else {
          alert("Failed to submit your rating. Please try again later.");
        }
      } catch (error) {
        console.error("Error submitting voting:", error);
        alert(
          "An error occurred while submitting your voting. Please try again later."
        );
      }
    },

    copyMessage(text) {
      // Create a textarea element to copy the text to the clipboard
      const textarea = document.createElement("textarea");
      textarea.value = text;
      document.body.appendChild(textarea);

      // Select the text in the textarea and copy it to the clipboard
      textarea.select();
      document.execCommand("copy");

      // Remove the textarea
      document.body.removeChild(textarea);
      alert("copied to clipboard");
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
.thumbButt {
  background-color: white;
}
.thumbs {
  justify-content: flex-end;
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

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
  bottom: 6.7%;
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
  bottom: 6%;
  left: 2.5%;
  border: none;
  border-radius: 50px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding: 15px;
  outline: none;
  padding-right:5vh;
}
.question-input:focus {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.clear-chat-button {
  position: fixed;
  top: 9.3%;
  right: 10px;
}

.clear-chat-button ion-icon {
  color: #f07812;
  font-size: 22px;
}
.chat-container {
  display: flex;
  margin: 6px 0.5%;
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
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 20px;
  padding: 15px;
  background-color: #fff;
  max-width: 70%;
}

.messages {
  overflow-y: scroll;
  height: 66vh;
  padding-bottom: 30px;
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
  .thumbs {
    margin-top: 0px;
  }
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
    height: 58vh;
    padding-bottom: 30px;
  }
}
@media (max-width: 450px) {
  input::placeholder {
    font-size: 0.7rem;
  }

  .clear-chat-button {
    margin-top: 5px;
  }

}
</style>
