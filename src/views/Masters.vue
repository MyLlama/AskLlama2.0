<template>
  <ion-page>
    <ion-header :translucent="true" class="ion-no-border">
      <ion-toolbar mode="ios">
        <ion-title>Select Masters</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div v-for="category in mastersCategory" :key="category?.title">
        <MasterList
          :title="category.title"
          :masters="category.masters"
          :selectedMasters="selectedMasters"
          @selectedMastersChange="updateSelectedMasters"
        />
      </div>
    
    <div class="done-button">
      <button class="button-87" role="button" @click="saveSelectedMasters">
        Done
      </button>
    </div>

    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import MasterList from "./Masterlist.vue";

export default {
  name: "Master",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar, 
    MasterList,
  },

  data() {
    return {
      selectedMasters: [],
      mastersCategory: [
        {
          title: 'Prophets',
          masters: [
            {
              name: "Mohammed",
              selected: false,
              image: "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt: "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Buddha",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Jesus",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Krishna",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Mahavira",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Guru Nanak",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
          ]
        }, 
        {
          title: "Contemporary Masters",
          masters: [
            {
              name: "Eckhart tolle",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Mooji",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Thich naht han",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Sadhguru",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Swami Vivekananda",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Sri Sri Ravishanka",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "J. Krishnamurthi ",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Ram Dass",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Alan watts",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Sri Aurobindo",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Ramana MahaRishi ",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
          ]
        },
        {
          title: "Mystics of the Past",
          masters: [
            {
              name: "RamKrishna Paramhansa",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Swami Sivananda",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "RabindraNath Tagore",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "UG Krishnamurthy ",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Sri M",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Daaji",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Swami Satyananda Saraswati",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Swami Dayananda Saraswati",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Swami Dayananda Saraswati",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Paramhansa Yogananda",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Kabir Das",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Lao Tzu",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Zen Master Banki ",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Roomi",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Sufi Master X",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
          ]
        },
        {
          title: "Western Philosophers",
          masters: [
            {
              name: "Socrates",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Aristotle",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Plato",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Kant",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Hegel",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Nietzche",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Schoppenhier",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
          ]
        },
        {
          title: "Psychologists",
          masters: [
            {
              name: "Freud",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Jung",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Einstien",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Feynman",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
          ]
        },
        {
          title: "Fictional Chars",
          masters: [
            {
              name: "Dumbledore",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Oogway",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Alfred Batman ",
              selected: false,
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Yoda Star wars",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Morpheus",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Gandalf",
              image:
                "https://cdn.pixabay.com/photo/2023/06/23/08/51/lord-krishna-8083043_1280.png",
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
          ]
        }
      ]
    };
  },
  methods: {
    updateSelectedMasters(selectedMasters) {
      this.selectedMasters = selectedMasters;
    },
    saveSelectedMasters() {
      localStorage.setItem(
        "selectedMasters",
        JSON.stringify(this.selectedMasters)
      );
    },
  },
};
</script>
<style scoped>
ion-toolbar {
  --background: #19422d;
}
.master-container {
  background-color: #f07812;
}
.master-header {
  padding: 10px;
  display: flex;
  background-color: #f07812;
  color: black;
  font-family: "Trebuchet MS", sans-serif;
}
.master-header h1 {
  margin: auto;
}
.back-icon > img {
  width: 100%;
  width: 30px;
  height: 30px;
}

.button-87 {
  margin: auto;
  font-size: 15px;
  padding: 10px 20px;
  text-align: center;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  border-radius: 50px;
  display: block;
  border: 0px;
  font-weight: 700;
  box-shadow: 0px 0px 14px -7px #f09819;
  background-image: linear-gradient(
    45deg,
    #ff512f 0%,
    #f09819 51%,
    #ff512f 100%
  );
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-87:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
  letter-spacing: 0.3em;
}

.button-87:active {
  transform: scale(0.95);
}

@media (max-width: 768px) {
}
</style>
