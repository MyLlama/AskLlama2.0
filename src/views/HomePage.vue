<template>
  <ion-page>
    <ion-menu side="start" content-id="main-content">
      <ion-header>
        <ion-toolbar>
          <ion-back-button slot="start" text="" default-href="/home" />
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <ion-list>
          <ion-item @click="navigateTo('/master')">
            <ion-label>Select Masters</ion-label>
          </ion-item>
          <ion-item @click="navigateTo('/home')">
            <ion-label
              ><a class="about-us" href="https://www.myllama.co/"
                >About Us</a
              ></ion-label
            >
          </ion-item>

          <ion-item @click="showFeedback">
            <ion-label>Feedback</ion-label>
          </ion-item>

          <ion-item @click="navigateTo('/home')">
            <ion-label>Share</ion-label>
          </ion-item>

          <ion-item @click="showPrivacyPolicy">
            <ion-label>Privacy Policy</ion-label>
          </ion-item>

          <ion-item @click="showRating">
            <ion-label>Rate Us</ion-label>
          </ion-item>
        </ion-list>
      </ion-content>
    </ion-menu>

    <ion-header class="ion-no-border">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button auto-hide="false"></ion-menu-button>
        </ion-buttons>
        <img class="header-logo" src="../assets/llama-lgo.png" alt="" />
        <ion-title class="header-title" mode="ios">
          AskLlama
          <p class="subtitle">Modern Problems. Timeless Answers.</p>
        </ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true" id="main-content">
      <chatbox
        :selectedMasters="selectedMasters"
        :selectedMastersCount="selectedMasters.length"
      ></chatbox>
    </ion-content>

    <!-- disclaimer -->
    <the-disclaimer v-show="isDisclaimerVisible" @close="closeDisclaimer">
      <template v-slot:header>
        <h2>Disclaimer</h2>
      </template>
      <template #body>
        <ul class="custom-bullet">
          <br />

          <li>
            AskLlama is an artificial intelligence program that doesn’t take
            itself too seriously. Hope you don't too 🙂 🙃
          </li>
          <br />
          <li>
            As much as we love our AskLlama characters, they are not the
            originals but only representations. Don't worry though, they still
            have all the personality and charm of the original Masters 😎
          </li>
          <br />
          <li>
            AskLlama responses are for informational purposes only and should
            not be treated as sage advice. So, if you're looking to quit your
            job and become a llama herder because of something we said, maybe
            double check with an actual professional first.
          </li>
          <br />
          <li>
            AskLlama may occasionally provide inaccurate information or use
            humour (our best quality obviously) that may not be everyone’s cup
            of tea.
          </li>
          <br />

          <br />
          <p>
            Ask away, but don't sue us if it gets sassy! We're just a bunch of
            llamas trying to make your day a little brighter!
          </p>
        </ul>
      </template>
    </the-disclaimer>
    

    <PrivacyPolicy ref="privacyPolicy" />
    <Rating ref="rating" />
    <Feedback ref="feedback" />
  </ion-page>
</template>

<script>
import Chatbox from "@/views/Chatbox.vue";
import TheDisclaimer from "./TheDisclaimer.vue";
import Feedback from "../views/Feedback.vue";
import Rating from "../views/Rating.vue";
import PrivacyPolicy from "../views/Privacy.vue";
import Disclaimer from "../views/Disclaimer.vue";

import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonMenuButton,
  IonButtons,
  IonList,
  IonItem,
  IonLabel,
} from "@ionic/vue";

export default {
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonMenuButton,
    IonButtons,
    IonList,
    IonItem,
    IonLabel,
    Chatbox,
    TheDisclaimer,
    Feedback,
    Rating,
    PrivacyPolicy,
    Disclaimer,
  },
  data() {
    return {
      isDisclaimerVisible: true,
      thankYouMessage: false,

      selectedMasters: [
        {
          name: "Krishna",
          image:
            "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
          selected: false,
          prompt:
            "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
        },
      ],
    };
  },

  methods: {
    navigateTo(path) {
      this.$router.push(path);
      this.$menuController.close();
    },
    showDisclaimer() {
      this.isDisclaimerVisible = true;
    },
    closeDisclaimer() {
      this.isDisclaimerVisible = false;
    },
    showRating() {
      this.$refs.rating.show();
    },
    showPrivacyPolicy() {
      this.$refs.privacyPolicy.show();
    },
    showFeedback() {
      this.$refs.feedback.show();
    },
  },
};
</script>

<style scoped>
.header-title {
  font-size: 1.5rem;
}
ion-item {
  cursor: pointer;
}
h2 {
  font-family: "Trebuchet MS", sans-serif;
}
ion-toolbar {
  --background: #f07812;
  --color: #fff;
  --min-height: 60px;
}
ion-page {
  font-family: "Trebuchet MS", sans-serif;
}

.about-us {
  text-decoration: none;
  color: #f07812;
}
.subtitle {
  font-size: 60%;
  color: black;
}

.header-logo {
  border-radius: 100%;
  width: 50px;
  height: auto;
  position: relative;
  left: 37%;
  bottom: auto;
  text-align: center;
}

ul.custom-bullet {
  list-style-type: none;
}

ul.custom-bullet li::before {
  content: "✔ ";
  color: green;
  font-weight: bold;
}

@media (max-width: 767px) {
  .header-logo {
    display: none;
  }
  textarea {
    width: 95%;
  }
}
</style>
