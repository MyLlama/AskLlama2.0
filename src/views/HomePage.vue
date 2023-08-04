<template>
  <ion-page>
    <ion-header class="ion-no-border">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button auto-hide="false"></ion-menu-button>
        </ion-buttons>
        <img class="header-logo" src="../../public/img/llama-logo.png" alt="">
        <ion-title mode="ios"> 
          AskLlama
          <p class="subtitle">Modern Problems. Timeless Answers.</p>
        </ion-title>
        
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <chatbox :selectedMasters="selectedMasters" :selectedMastersCount="selectedMasters.length"></chatbox>

    </ion-content>
  </ion-page>
</template>

<script>
import Chatbox from "@/views/Chatbox.vue";
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonMenuButton, IonButtons } from '@ionic/vue';
export default {
  components: {
    IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonMenuButton, IonButtons, Chatbox
  },
  data() {
    return {
      selectedMasters: [{
          name: "Krishna",
          image: "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
          selected: false,
          prompt:
            "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
        }],

    }
  }
}
</script>

<style scoped>
ion-toolbar {
  --background: #F07812;
  --color: #fff;
  --min-height: 60px;
 
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
  text-align:center;
}
</style>
