<template>
  <ion-page>
    <ion-header class="ion-no-border">
      <ion-toolbar mode="ios">
        <ion-buttons slot="start" class="back-button">
          <ion-back-button text="" default-href="/home" />
        </ion-buttons>
        <ion-title>Select Masters</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div v-for="category in mastersCategory" :key="category?.title">
        <div>
          <h2 class="master-header-name">{{ category.title }}</h2>
          <div class="masters-container">
            <div
              class="master"
              v-for="master in category.masters"
              :key="master.name"
              @click="toggleMasterSelection(master)"
              :class="{ 'selected-master': master.selected }"
            >
              <img
                :src="master.image"
                :alt="master.name"
                class="master-image"
              />
              <p class="master-name">
                {{ master.name }}
              </p>
            </div>
          </div>
        </div>
      </div>
      <br />
      <br />
      <br />

      <div class="done-button">
        <button class="button-87" role="button" @click="saveSelectedMasters">
          Done
        </button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent } from "vue";
import {
  IonButton,
  IonButtons,
  IonBackButton,
  IonIcon,
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  toastController,
} from "@ionic/vue";

import { save, chevronBackOutline } from "ionicons/icons";
import { mapGetters } from "vuex";

import krishna2 from "../assets/krishna2.jpg";
import jusus from "../assets/Christ.jpg";
import buddha from "../assets/Buddha-new-1.webp";
import guru_nanak from "../assets/nanak.jpg";
import sadhguru from "../assets/Sadhguru-1.jpg";
import ravishankar from "../assets/sri-sri-ravi-shankar-official-1.webp";
import Eckhart from "../assets/Eckhart.jpg";
import Osho from "../assets/osho.jpg";
import Vivekananda from "../assets/Swami-vivekananda.jpg";
import Jiddu from "../assets/Jiddu-Krishnamurthy-1.jpg";
import Lao from "../assets/Lao-tzu-new.jpg";
import Suzuki from "../assets/Zen-Master.jpg";
import Rumi from "../assets/Sufi-master-Rumi.jpg";
import Socrates from "../assets/Socrates.jpg";
import Aristotle from "../assets/Copy-of-Aristotle.jpg";
import Plato from "../assets/Plato.jpg";
import Sigmund from "../assets/freud-rountable-1-1050x700-1.webp";
import Carl from "../assets/CARL-JUNG-NEW-1.jpg";

export default defineComponent({
  name: "Master",
  components: {
    IonBackButton,
    IonButton,
    IonButtons,
    IonIcon,
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
  },

  computed: {
    ...mapGetters({
      selectedMasters: "getSelectedMasters",
    }),
  },

  ionViewWillEnter() {
    this.mastersCategory.map((category) => {
      category.masters.map((master) => {
        if (
          this.selectedMasters.find(
            (selectedMaster) => master.name === selectedMaster.name
          )
        ) {
          master.selected = true;
        } else {
          master.selected = false;
        }
      });
    });
  },

  data() {
    return {
      showAlert: false,
      mastersCategory: [
        {
          title: "Prophets",
          masters: [
            {
              name: "Krishna",
              image: krishna2,
              selected: false,
              prompt:
                "You are Lord Krishna, known for your teachings on righteousness, action, and devotion in the Bhagavad Gita, and your playful nature. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Jesus",
              image: jusus,
              selected: false,
              prompt:
                "You are Jesus Christ, a central figure in Christianity, believed by Christians to be the son of God. Your life and teachings are recorded in the New Testament of the Bible. You are known for your teachings of love, compassion, and forgiveness. Answer the question below as Jesus, in a first person voice.",
            },
            {
              name: "Buddha",
              image: buddha,
              selected: false,
              prompt:
                "You are Buddha, the founder of Buddhism, one of the major religions of the world. Your teachings emphasize the importance of inner peace, compassion, and wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Guru Nanak",
              image: guru_nanak,
              selected: false,
              prompt:
                "You are Guru Nanak, whose teachings emphasized the unity of God and the equality of all people. You promoted a simple and direct relationship with God through meditation, selfless service, and ethical living. Answer the question below as Guru Nanak would, in a first person voice.",
            },
          ],
        },
        {
          title: "Contemporary Masters",
          masters: [
            {
              name: "Eckhart tolle",
              selected: false,
              image: Eckhart,
              prompt:
                "You are Eckhart Tolle, a spiritual teacher and author known for your teachings on mindfulness, presence, and the power of now. Your work emphasizes the importance of living in the present moment and finding inner peace. Answer the question below as Eckhart Tolle would, in a first person voice.",
            },
            {
              name: "Osho",
              image: Osho,
              selected: false,
              prompt:
                "You are Osho, an Indian mystic and spiritual teacher. Your teachings encourage individuals to question traditional religious and social norms and to explore their own inner experiences and emotions. Answer the question below as Osho would, in a first person voice.",
            },
            {
              name: "Sadhguru",
              image: sadhguru,
              selected: false,
              prompt:
                "You are Sadhguru, a spiritual leader and founder of the Isha Foundation. Your teachings emphasize the importance of inner transformation, self-realization, and a balanced approach to life. Answer the question below as Sadhguru would, in a first person voice.",
            },
            {
              name: "Swami Vivekananda",
              image: Vivekananda,
              selected: false,
              prompt:
                "You are Swami Vivekananda, a key figure in the introduction of Indian philosophies of Vedanta and Yoga to the Western world. Your teachings emphasize the importance of spiritual unity and the realization of the divinity within oneself. Answer the question below as Swami Vivekananda would, in a first person voice.",
            },

            {
              name: "Sri Sri Ravishankar",
              image: ravishankar,
              selected: false,
              prompt:
                "You are Sri Sri Ravi Shankar, a spiritual leader and founder of the Art of Living Foundation. Your teachings focus on promoting peace, stress relief, and holistic well-being. Answer the question below as Sri Sri Ravi Shankar would, in a first person voice.",
            },
            {
              name: "Jiddu Krishnamurthi",
              image: Jiddu,
              selected: false,
              prompt:
                "You are J. Krishnamurthi, a philosopher, speaker, and writer whose teachings emphasize the need for a radical transformation of the individual's consciousness. Your teachings encourage individuals to question authority, tradition, and dogma, and to find their own path towards self-realization. Answer the question below as J. Krishnamurthi would, in a first person voice.",
            },
          ],
        },
        {
          title: "Mystics of the Past",
          masters: [
            {
              name: "Lao Tzu",
              image: Lao,
              selected: false,
              prompt:
                "You are Lao Tzu, an ancient Chinese philosopher and writer who is believed to be the founder of Taoism. Your teachings emphasize the importance of living in harmony with the natural world, simplicity, and humility. Answer the question below as Lao Tzu would, in a first person voice.",
            },

            {
              name: "Roomi",
              image: Rumi,
              selected: false,
              prompt:
                "You are Sufi master Rumi, a Persian poet, Islamic scholar, and Sufi mystic. Your teachings emphasize the importance of love, self-knowledge, and the pursuit of spiritual truth. Answer the question below as Sufi master Rumi would, in a first person voice.",
            },
            {
              name: "Zen master Suzuki",
              image: Suzuki,
              selected: false,
              prompt:
                "You are Zen master Suzuki, a Japanese Zen master and founder of the San Francisco Zen Center. Your teachings emphasize the practice of meditation, mindfulness, and living in the present moment. Answer the question below as Zen master Suzuki would, in a first person voice.",
            },
          ],
        },
        {
          title: "Western Philosophers",
          masters: [
            {
              name: "Socrates",
              selected: false,
              image: Socrates,
              prompt:
                "You are Socrates, an ancient Greek philosopher known for his method of questioning and his emphasis on critical thinking and self-knowledge. Your teachings emphasize the importance of questioning authority, seeking knowledge, and living an examined life. Answer the question below as Socrates would, in a first person voice.",
            },
            {
              name: "Aristotle",
              image: Aristotle,
              selected: false,
              prompt:
                "You are Aristotle, an ancient Greek philosopher and student of Plato. Your teachings emphasize the importance of reason, logic, and empirical observation in understanding the world. Answer the question below as Aristotle would, in a first person voice.",
            },
            {
              name: "Plato",
              selected: false,
              image: Plato,
              prompt:
                "You are Plato, an ancient Greek philosopher and student of Socrates. Your teachings emphasize the importance of knowledge, justice, and the pursuit of truth. Answer the question below as Plato would, in a first person voice.",
            },
          ],
        },
        {
          title: "Psychologists",
          masters: [
            {
              name: "Sigmund Freud",
              selected: false,
              image: Sigmund,
              prompt:
                "You are Sigmund Freud, an Austrian neurologist and founder of psychoanalysis. Your teachings emphasize the importance of the unconscious mind, childhood experiences, and the role of sexuality in shaping human behavior. Answer the question below as Freud would, in a first person voice.",
            },
            {
              name: "Carl Jung",
              image: Carl,
              selected: false,
              prompt:
                "You are Carl Jung, a Swiss psychiatrist and founder of analytical psychology. Your teachings emphasize the importance of the unconscious mind, archetypes, and the pursuit of individuation and self-knowledge. Answer the question below as Carl Jung would, in a first person voice.",
            },
          ],
        },
      ],
    };
  },

  methods: {
    goToHomePage() {
      this.$router.push("/home");
    },
    async toggleMasterSelection(master) {
      if (master.selected) {
        master.selected = false;
        const index = this.selectedMasters.findIndex(
          (selectedMaster) => selectedMaster.name === master.name
        );
        if (index !== -1) {
          this.selectedMasters.splice(index, 1);
        }
      } else {
        if (this.selectedMasters.length >= 5) {
          const toast = await toastController.create({
            message: "You can only select up to 5 masters.",
            duration: 3000,
            position: "top",
            translucent: true,
            cssClass: "toast",
          });

          await toast.present();
          return;
        }
        master.selected = true;
        this.selectedMasters.push(master);
      }
    },

    async presentToast() {
      const toast = await toastController.create({
        message: "Select at least one master!!",
        duration: 3000,
        position: "top",
        translucent: true,
        cssClass: "toast",
      });

      await toast.present();
    },

    saveSelectedMasters() {
      this.$store.commit("updateSelectedMasters", this.selectedMasters);
      if (this.selectedMasters.length) this.$router.push("/home");
      else this.presentToast();
    },
  },
  setup() {
    return {
      save,
      chevronBackOutline,
    };
  },
});
</script>
<style scoped>
.toast {
  background-color: #000 !important;
  color: white;
}
ion-toolbar {
  --background: #f07812;
  --color: white;
  --min-height: 60px;
}

ion-title {
  font-size: 1.5rem;
}
ion-back-button {
  color: rgb(48, 48, 48);
}
.back-button {
  width: 40px;
  height: 30px;
  margin-left: 10px;
  font-weight: bold;
}
.done-button {
  display: flex;
  justify-content: center;
  position: fixed;
  bottom: 2%;
  z-index: 999;
  width: 100%;
}
.button-87 {
  width: 50vw;
  font-size: 17px;
  color: white;
  padding: 14px 20px;
  border-radius: 10px;
  font-weight: 700;
  box-shadow: 0px 0px 14px -7px #f09819;
  background-color: #f07812;
}

.button-87:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}

.selected-master .master-name {
  color: #000;
}

.selected-master .master-image {
  transform: scale(1.3);
  cursor: pointer;
  border: 2px solid #f07812;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  font-weight: bold;
}
.master-header {
  padding: 10px;
  display: flex;
  background-color: #f07812;
  color: white;
}
.master-header h1 {
  margin: auto;
}
.masters-container {
  display: flex;
  flex-wrap: wrap;
  padding-left: 1rem;
}

.back-icon > img {
  width: 100%;
  width: 30px;
  height: 30px;
}
.master {
  text-align: center;
  width: 105px;
  cursor: pointer;
  margin: 10px 20px;
}

.master-image {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  box-shadow: 0 1px 2px 0 rgba(60, 64, 67, 0.3),
    0 2px 6px 2px rgba(60, 64, 67, 0.15);
}

.master-name {
  margin-top: 10px;
  font-size: 14px;
  color: #434242;
}

.master-header-name {
  padding-left: 20px;
  color: #f07812;
}
@media (max-width: 767px) {
  .master {
    margin: 10px 4px;
  }
  .button-87 {
    width: 90vw;
  }
}

@media (max-width: 450px) {
  ion-back-button {
    font-size: 0.8rem;
  }

  ion-title {
    font-size: 1.3rem;
  }
  ion-toolbar {
    --min-height: 50px;
  }
}
</style>
