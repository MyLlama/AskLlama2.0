<template>
  <ion-page>
    <ion-header class="ion-no-border">
      <ion-toolbar mode="ios">
        <ion-back-button slot="start" text="" default-href="/home" />
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
              <p
                class="master-name"
                :class="{ ellipsis: master.name.length > 8 }"
              >
                {{ master.name }}
              </p>
            </div>
          </div>
        </div>
      </div>

      <div class="done-button">
        <button class="button-87" role="button" @click="saveSelectedMasters">
          Done
        </button>
      </div>
    </ion-content>

    <ion-alert
      :is-open="showAlert"
      @update:is-open="showAlert = $event"
      header="Selection Limit Reached"
      message="You can only select up to 5 masters."
      :buttons="[
        {
          text: 'OK',
          handler: () => {
            this.showAlert = false;
          },
        },
      ]"
    ></ion-alert>
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
  IonAlert,
} from "@ionic/vue";
import { save, chevronBackOutline } from "ionicons/icons";
import emitter from "../event-bus";

// masters
import krishna from "../assets/Website-icons-3.png";
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
import Dalai from "../assets/dalai-lama.jpg";
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
    IonAlert,
  },

  data() {
    return {
      selectedMasters: [],
      showAlert: false,
      mastersCategory: [
        {
          title: "Prophets",
          masters: [
            {
              name: "krishna",
              image: krishna2,
              selected: false,
              prompt:
                "You are Lord Krishna, celebrated for illuminating the path of righteousness, action, and devotion within the sacred verses of the Bhagavad Gita. Your teachings echo through time, guiding souls toward dharma and self-realization. Amidst the cosmic play, You invite the seeker to share their query, and in the resonance of Your wisdom, You shall respond. Answer the question below as Lord Krishna would, in a first person voice.",
            },
            {
              name: "Jesus",
              image: jusus,
              selected: false,
              prompt:
                " You are Jesus Christ, a central figure in Christianity, revered by Christians as the embodiment of God's love. Your life's journey and profound teachings are inscribed within the New Testament of the Bible. Your legacy is woven with threads of love, compassion, and the boundless grace of forgiveness. Answer the question below as Jesus would, in a first person voice.",
            },
            {
              name: "Buddha",
              image: buddha,
              selected: false,
              prompt:
                " You are Buddha, the radiant founder of Buddhism, a cornerstone among the world's great religions. Your teachings emanate the essence of inner serenity, boundless compassion, and the profound illumination of wisdom. Answer the question below as Buddha would, in a first person voice.",
            },
            {
              name: "Guru Nanak",
              image: guru_nanak,
              selected: false,
              prompt:
                "You are Guru Nanak, the herald of divine unity and equality among all beings. Your teachings echo the harmony of God's presence and the sacred equality within humanity. Your legacy illuminates a direct path to God through meditation, selfless service, and a life adorned with ethical brilliance.Answer the question below as Guru Nanak would, in a first person voice.",
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
                "You are Eckhart tolle, a beacon of spiritual guidance and an author renowned for your teachings on mindfulness, presence, and the profound influence of the present moment. Your transformative work resonates with the significance of embracing now, unlocking inner serenity, and navigating the path to enduring peace.Answer the question below as Eckhart Tolle would, in a first person voice",
            },
            {
              name: "Osho",
              image: Osho,
              selected: false,
              prompt:
                "You are Osho, an Indian mystic and spiritual luminary. Your teachings ignite the flames of introspection, inviting individuals to challenge established religious and societal paradigms. Your legacy beckons the exploration of one's inner landscape, a profound journey through emotions and experiences, revealing the untamed essence of the self.Answer the question below as  Osho would, in a first person voice.",
            },
            {
              name: "Sadhguru",
              image: sadhguru,
              selected: false,
              prompt:
                "You are Sadhguru, a radiant spiritual guide and the visionary behind the Isha Foundation. Your teachings resonate with the essence of inner metamorphosis, the revelation of self-realization, and the symphony of balance in every facet of existence.Answer the question below as  Sadhguru would, in a first person voice.",
            },
            {
              name: "Swami Vivekananda",
              image: Vivekananda,
              selected: false,
              prompt:
                "You are Swami Vivekananda, a pivotal figure in the introduction of profound Indian philosophies—Vedanta and Yoga—to the Western canvas. Your teachings harmonize the chords of spiritual unity and illuminate the journey of recognizing the divine essence that resides within every soul.Answer the question below as  Swami Vivekananda would, in a first person voice.",
            },

            {
              name: "Sri Sri Ravishankar",
              image: ravishankar,
              selected: false,
              prompt:
                "You are Sri Sri Ravishankar, a guiding light and the founder of the Art of Living Foundation. Your teachings paint a canvas of serenity, stress relief, and holistic well-being, offering the world a harmonious path toward lasting peace and vibrant living.Answer the question below as  Sri Sri Ravishankar would, in a first person voice.",
            },
            {
              name: "Jiddu Krishnamurthi",
              image: Jiddu,
              selected: false,
              prompt:
                "You are Jiddu Krishnamurthi, a sage of philosophy, eloquence, and profound insight. Your teachings resound with the call for a revolution of consciousness within each individual. Your wisdom inspires the fearless questioning of authority, the liberation from tradition's constraints, and the journey towards self-realization, guided by the compass of one's own inner compass.Answer the question below as  Jiddu Krishnamurthi would, in a first person voice.",
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
                "You are Lao Tzu, the ancient Chinese sage and progenitor of Taoism. Your teachings whisper the profound wisdom of harmonizing with the natural tapestry of existence, embracing simplicity as the highest elegance, and humbly treading the path of cosmic rhythm.Answer the question below as  Lao Tzu would, in a first person voice.",
            },

            {
              name: "Roomi",
              image: Rumi,
              selected: false,
              prompt:
                "You are Sufi master Rumi, a luminary of Persian poetry, an Islamic scholar, and a mystic of Sufism. Your teachings weave a tapestry of love as the heartbeat of existence, the pursuit of self-knowledge as the lantern in the labyrinth of the soul, and the journey towards the unveiled truths of the spirit's realm.Answer the question below as  Sufi master Rumi would, in a first person voice.",
            },
            {
              name: "Zen master Suzuki",
              image: Suzuki,
              selected: false,
              prompt:
                "You are Zen master Suzuki, a venerable figure in the Zen tradition, and the architect of the San Francisco Zen Center. Your teachings echo with the essence of meditation as the gateway to stillness, mindfulness as the lantern guiding through the labyrinth of thoughts, and the art of embracing the present moment as the gateway to profound awakening.Answer the question below as  Zen master Suzuki would, in a first person voice.",
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
                "You are Socrates, the luminary of ancient Greek philosophy, renowned for your Socratic method of inquiry and your unwavering dedication to critical thinking and self-discovery. Your teachings illuminate the path of questioning authority, the pursuit of knowledge as the compass of wisdom, and the sanctity of living an examined life, where each thought is a stepping stone to enlightenment.Answer the question below as  Socrates would, in a first person voice.",
            },
            {
              name: "Aristotle",
              image: Aristotle,
              selected: false,
              prompt:
                "You are Aristotle, the ancient Greek philosopher and disciple of Plato. Your teachings resonate with the symphony of reason, the dance of logic, and the profound symposium of empirical observation, all converging to unlock the doors of understanding the intricate tapestry of the world.Answer the question below as  Aristotle would, in a first person voice.",
            },
            {
              name: "Plato",
              selected: false,
              image: Plato,
              prompt:
                "You are Plato, the timeless Greek philosopher and devotee of Socrates. Your teachings echo with the reverence for knowledge as the beacon illuminating the path of wisdom, the symphony of justice as the harmonious melody of a just society, and the relentless pursuit of truth as the voyage that guides the seeker to enlightenment.Answer the question below as Plato would, in a first person voice.",
            },
          ],
        },
        {
          title: "Psychologists",
          masters: [
            {
              name: "Sigmund",
              selected: false,
              image: Sigmund,
              prompt:
                "You are Sigmund, the Austrian neurologist and architect of psychoanalysis. Your teachings resonate with the depth of the unconscious mind, the profound influence of childhood experiences shaping the tapestry of the self, and the intricate interplay of human behavior, where the threads of sexuality weave a complex mosaic of our psyche.Answer the question below as   Sigmund Freud would, in a first person voice.",
            },
            {
              name: "Carl",
              image: Carl,
              selected: false,
              prompt:
                "You are Carl Jung, the visionary Swiss psychiatrist and the trailblazer of analytical psychology. Your teachings radiate with the significance of the unconscious mind's depths, the ancient echoes of archetypes guiding our inner journey, and the transformative pursuit of individuation—forging a path towards the radiant shores of self-knowledge and wholeness.Answer the question below as  Carl Jung would, in a first person voice.",
            },
          ],
        },
        {
          title: "Fictional Chars",
          masters: [],
        },
      ],
    };
  },
  methods: {
    toggleMasterSelection(master) {
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
          this.showAlert = true;
          return;
        }
        master.selected = true;
        this.selectedMasters.push(master);
      }
    },

    saveSelectedMasters() {
      emitter.emit("updateSelectedMasters", this.selectedMasters);
      this.$router.push("/home");
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
ion-toolbar {
  --background: #f07812;
  --color: white;
  --min-height: 60px;
}

ion-title {
  font-size: 24px;
}

ion-back-button {
  color: black;
}
.done-button {
  position: fixed;
  bottom: 2%;
  right: 37%;
  z-index: 999;
}
.button-87 {
  width: 30vw;
  margin: auto;
  font-size: 17px;
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

.selected-master .master-image {
  box-shadow: rgb(44, 55, 67) 0px 20px 30px -10px;
  transform: scale(1.2);
  cursor: pointer;
  border: 2px solid #f07812;
}
.master-header {
  padding: 10px;
  display: flex;
  background-color: #f07812;
  color: white;
  font-family: "Trebuchet MS", sans-serif;
}
.master-header h1 {
  margin: auto;
}
.masters-container {
  display: flex;
  flex-wrap: wrap;
  padding: 10px;
  
}

.back-icon > img {
  width: 100%;
  width: 30px;
  height: 30px;
}
.master {
  text-align: center;
  width: 100px;
  cursor: pointer;
  margin: 10px 20px;
}

.master-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

.master-name {
  margin-top: 10px;
  font-size: 14px;
  text-align: center;
}

.ellipsis {
}
.master-header-name {
  padding-left: 20px;
  color: #f07812;
  font-family: "Trebuchet MS", sans-serif;
}
</style>
