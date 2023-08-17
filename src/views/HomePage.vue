<template>
  <ion-page>
    <ion-menu side="start" content-id="main-content">
      <ion-toolbar class="menu-header">
        <ion-menu-toggle>
          <img class="back-button" src="../assets/backButton.png" />
        </ion-menu-toggle>
      </ion-toolbar>
      <ion-content>
        <ion-list>
          <ion-item lines="none" @click="navigateTo('/master')">
            <ion-label class="about-us">Select Masters</ion-label>
          </ion-item>
          <ion-item lines="none">
            <ion-label
              ><a class="about-us" href="https://www.myllama.co/"
                >About Us</a
              ></ion-label
            >
          </ion-item>

          <!-- <ion-item lines="none" @click="showFeedback">
            <ion-label class="about-us">Feedback</ion-label>
          </ion-item> -->

          <!-- <ion-item lines="none" @click="navigateTo('/home')">
            <ion-label class="about-us">Share</ion-label>
          </ion-item> -->

          <ion-item lines="none" @click="showPrivacyPolicy">
            <ion-label class="about-us">Privacy Policy</ion-label>
          </ion-item>

          <!-- <ion-item lines="none" @click="showRating">
            <ion-label class="about-us">Rate Us</ion-label>
          </ion-item> -->
        </ion-list>
      </ion-content>
    </ion-menu>

    <ion-header class="ion-no-border">
      <ion-toolbar class="ion-toolbar-header">
        <ion-buttons slot="start">
          <ion-menu-button auto-hide="false"></ion-menu-button>
        </ion-buttons>

        <ion-item lines="none" class="header-title">
          <img class="header-logo" src="../assets/llama-lgo.png" alt="" />
          <ion-title class="main-title" mode="ios">
            AskLlama
            <p class="subtitle">Modern Problems. Timeless Answers.</p>
          </ion-title>
        </ion-item>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" id="main-content">
      <div class="selected-masters-container">
        <div class="selected-masters">
          <div
            class="master-info"
            v-for="(master, index) in selectedMasters"
            :key="master"
          >
            <div class="master-content">
              <p
                @click.stop="removeMaster(index)"
                class="remove_master_button"
              >
                ×
              </p>
              <img :src="master.image" :alt="master.name" />
            </div>
          </div>
          <div
            @click="this.$router.push('/master')"
            class="add_button"
            v-if="selectedMasters.length<5"
          >
            <p>+</p>
          </div>
        </div>
      </div>

      <chatbox
        class="chatbox-homepage"
        :selectedMasters="selectedMasters"
        :selectedMastersCount="selectedMasters.length"
      ></chatbox>
      <div class="footer">
        <a class="footer-link" href="https://www.myllama.co/">
          Join Llama's programs to awaken your inner wisdom🌻
        </a>
      </div>
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
        <br />
      </template>
      <br />
      <br />
    </the-disclaimer>

    <PrivacyPolicy ref="privacyPolicy" />
    <Rating ref="rating" class="rating_" />
    <Feedback ref="feedback" />
  </ion-page>
</template>

<script>
import Chatbox from "@/views/Chatbox.vue";
import TheDisclaimer from "./TheDisclaimer.vue";
import Feedback from "../views/Feedback.vue";
import Rating from "../views/Rating.vue";
import PrivacyPolicy from "../views/Privacy.vue";
import { mapGetters } from 'vuex'

import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonMenu,
  IonMenuButton,
  IonButtons,
  IonList,
  IonItem,
  IonLabel,
  IonMenuToggle,
  menuController,
} from "@ionic/vue";

export default {
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonMenu,
    IonMenuButton,
    IonMenuToggle,
    IonButtons,
    IonList,
    IonItem,
    IonLabel,
    Chatbox,
    TheDisclaimer,
    Feedback,
    Rating,
    PrivacyPolicy,
    menuController,
  },
  data() {
    return {
      isDisclaimerVisible: true,
    };
  },
  computed: {
    ...mapGetters({
      selectedMasters: 'getSelectedMasters'
    })
  },
  methods: {
    async navigateTo(path) {
      this.$router.push(path);
      await menuController.toggle();
    },
    showDisclaimer() {
      this.isDisclaimerVisible = true;
    },
    closeDisclaimer() {
      this.isDisclaimerVisible = false;
      this.$router.push('/master');
    },
    async showRating() {
      this.$refs.rating.show();
      await menuController.toggle();
    },
    async showPrivacyPolicy() {
      this.$refs.privacyPolicy.show();
      await menuController.toggle();
    },
    async showFeedback() {
      this.$refs.feedback.show();
      await menuController.toggle();
    },
    removeMaster(index) {
      this.selectedMasters.splice(index, 1);
      this.$store.commit('updateSelectedMasters', this.selectedMasters);
    },
  },
};
</script>

<style scoped>
ion-menu {
  width: 100%;
}

.menu-header {
  padding: 0vh;
  cursor: pointer;
  --background: #fff;
  height: 40px;
}
.about-us {
  text-decoration: none;
  color: #f07812;
  font-size: 1.3rem;
  padding-left: 1.2rem;
}
.about-us:hover {
  color: black;
}
ion-menu-button {
  color: rgb(48, 48, 48);
  font-size: 2rem;
}
.ion-no-border {
  padding: 5px;
}

.ion-no-border-menu {
  padding-left: 2px;
  padding-top: 5px;
}
.ion-toolbar-header {
  padding: 5px;
}
.back-button {
  padding: 0;
  margin: 0;
  width: 20px;
  height: 20px;
}
.footer-link {
  text-decoration: none;
  color: black;
}
.footer {
  position: fixed;
  bottom: 12px;
  right: 0;
  left: 0;
  text-align: center;
  font-size: 1rem;
}

ion-label {
  color: #f07812;
}
.header-logo {
  border-radius: 100%;
  width: 50px;
}
.main-title {
  font-size: 1.5rem;
  color: white;
}

.header-title {
  margin: auto;
  width: 550px;
  display: flex;
  justify-content: space-around;
  --background: #f07812;
}

ion-item {
  cursor: pointer;
}

ion-toolbar {
  --background: #f07812;
  --color: #fff;
  --min-height: 60px;
}

.chatbox-homepage {
  margin-top: 40px;
  height: fit-content;
}
.remove_master_button {
  margin-left: auto;
  text-align: right;
  font-weight: bold;
  visibility: hidden;
  height: 10px;
  width: 10px;
  font-size: 1.3rem;
  position: relative;
  bottom: 6px;
  left: 5px;
}
.selected-masters-container {
  max-width: 100%;
  height: 8vh;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 3px 0px,
    rgba(0, 0, 0, 0.06) 0px 1px 2px 0px;
}

.master-content:hover .remove_master_button {
  visibility: visible;
  cursor: pointer;
}

.selected-masters {
  height: 8vh;
  display: flex;
  align-items: center;
  flex-wrap: nowrap;
  padding: 10px;
}

.master-info {
  margin: 5px;
  text-align: center;
  flex: 0 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.master-content {
  text-align: center;
}
.back-button {
  height: 16px;
  width: 16px;
  margin-left: 10px;
  margin-top: 10px;
}

.selected-masters img {
  border-radius: 50%;
  max-width: 40px;
  height: auto;
  border: #f07812 solid;
  cursor: pointer;
}
.add_button {
  cursor: pointer;
  font-size: 2rem;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  margin-left: 5px;
  margin-top: 6px;
  box-shadow: rgba(17, 17, 26, 0.05) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 0px 8px;
}
.add_button p {
  border-radius: 50%;
  position: relative;
  left: 11px;
  bottom: 1px;
}


.subtitle {
  font-size: 1rem;
  color: black;
}

ul.custom-bullet {
  list-style-type: none;
}

ul.custom-bullet li::before {
  content: "•";
  color: black;
  font-weight: bold;
}

@media (max-width: 767px) {
  .header-logo {
    display: none;
  }
  textarea {
    width: 95%;
  }
  .header-title {
    width: 300px;
  }
  .main-title {
    font-size: 1.2rem;
  }
  .subtitle {
    font-size: 0.9rem;
    color: black;
  }

  .selected-masters-container {
    height: 8vh;
  }

  .selected-masters {
    height: 7vh;
  }
  .footer {
    font-size: 0.9rem;
    bottom: 8px;
  }
}

@media (max-width: 450px) {
  .header-title {
    width: 300px;
  }
  .main-title {
    font-size: 1rem;
  }
  .subtitle {
    font-size: 0.7rem;
    color: black;
  }
  .ion-toolbar-header {
    padding: 0px;
  }
  .footer {
    font-size: 0.7rem;
    bottom: 10px;
  }

  ion-menu-button {
    font-size: 1.5rem;
  }
}

/* @media (max-width: 380px) {
  .footer {
    font-size: 0.6rem;
    bottom: 6px;
  }
}
@media (max-width: 250px) {
  .header-title {
    width: 200px;
  }
  .main-title {
    font-size: 1rem;
  }
  .subtitle {
    font-size: 0.5rem;
    color: black;
  }
} */
</style>
