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
          <ion-item @click="navigateTo('/home')">
            <ion-label>Feedback</ion-label>
          </ion-item>
          <ion-item @click="navigateTo('/home')">
            <ion-label>Share</ion-label>
          </ion-item>
          <ion-item @click="navigateTo('/home')">
            <ion-label
              ><a class="about-us" @click.prevent="showPrivacyPolicy"
                >Privacy policy</a
              ></ion-label
            >
          </ion-item>
          <ion-item @click="navigateTo('/home')">
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

    <!-- Privacy Policy-->
    <the-disclaimer v-show="isPrivacyPolicyVisible" @close="closePrivacyPolicy">
      <template v-slot:header>
        <h2>Privacy Policy</h2>
      </template>

      <template #body>
        <p class="privacy-policy-content">
          At MyLlama, we value the privacy of our visitors. This Privacy Policy
          explains the types of information we collect and how we use it. If you
          have any additional questions or need more information, please don't
          hesitate to contact us. This Privacy Policy applies only to our online
          activities and is valid for visitors to our website with respect to
          the information they share and/or collect on MyLlama. It does not
          apply to any offline information or information collected through
          other channels. By using our website, you consent to our Privacy
          Policy and agree to its terms.
          <br />
          <br />

          <span>Information We Collect:</span> When you use our website, you may
          be asked to provide certain personal information. The reasons for
          collecting this information will be made clear to you at the time of
          collection. If you contact us directly, we may receive additional
          information such as your name, email address, phone number, the
          contents of your message, and any other information you choose to
          provide. When you register for an account, we may ask for your contact
          information, including items such as your name, company name, address,
          email address, and telephone number.
          <br />
          <br />

          <span>How We Use Your Information:</span> We use the information we
          collect for various purposes, including providing, operating, and
          maintaining our website, improving and personalizing user experiences,
          understanding and analyzing website usage, developing new products and
          services, communicating with users, and sending updates and
          promotional information. We may also use your information to prevent
          fraud.
          <br />
          <br />

          <span>Log Files: </span>
          MyLlama follows standard procedures for using log files. These files
          log visitors when they visit websites. The information collected may
          include internet protocol (IP) addresses, browser type, Internet
          Service Provider (ISP), date and time stamps, referring/exit pages,
          and possibly the number of clicks. This information is used for
          analyzing trends, administering the site, tracking user movement, and
          gathering demographic information. The collected information is not
          linked to any personally identifiable information.
          <br />
          <br />

          <span> Cookies and Web Beacons:</span>
          Like many other websites, MyLlama uses cookies to enhance user
          experiences and personalize web page content. Cookies store
          information about visitors' preferences and the pages they access or
          visit. This information is used to optimize the user experience by
          customizing content based on the visitor's browser type and other
          information.
          <br />
          <br />

          <span> Advertising Partners Privacy Policies:</span>
          Please consult the respective Privacy Policies of our advertising
          partners for detailed information. Third-party ad servers or ad
          networks may use technologies like cookies, JavaScript, or web beacons
          to personalize advertising content and measure the effectiveness of
          their campaigns. MyLlama has no access to or control over these
          cookies used by third-party advertisers.
          <br />
          <br />

          <span> Third-Party Privacy Policies:</span>
          MyLlama's Privacy Policy does not apply to other advertisers or
          websites. We recommend reviewing the Privacy Policies of third-party
          ad servers for detailed information on their practices and
          instructions on how to opt out of certain options. You can also
          disable cookies through your browser settings. Visit your browser's
          website for more information on managing cookies.
          <br />
          <br />

          <span>
            CCPA Privacy Rights (Do Not Sell My Personal Information):</span
          >
          Under the CCPA, California consumers have the right to request
          disclosure of the categories and specific pieces of personal data
          collected by a business, request deletion of personal data, and
          request a business that sells personal data not to sell their personal
          data. If you would like to exercise any of these rights, please
          contact us. We have one month to respond to your request.
          <br />
          <br />

          <span> GDPR Data Protection Rights:</span>
          You have the right to access, correct, erase, restrict processing,
          object to processing, and request data portability. If you would like
          to exercise any of these rights, please contact us. We have one month
          to respond to your request.
          <br />
          <br />

          <span>Children's Information:</span>
          Protecting children's privacy online is important to us. We encourage
          parents and guardians to monitor and guide their children's online
          activities. MyLlama does not knowingly collect personal identifiable
          information from children under the age of 13. If you believe that
          your child has provided personal information on our website, please
          contact us immediately, and we will make our best efforts to promptly
          remove such information from our records.
        </p>
      </template>
    </the-disclaimer>
  </ion-page>
</template>

<script>
import Chatbox from "@/views/Chatbox.vue";
import TheDisclaimer from "./TheDisclaimer.vue";
import TheDynamicDisclaimer from "./TheDynamicDisclaimer.vue";
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
    
  },
  data() {
    return {
      isPrivacyPolicyVisible: false,

      isDisclaimerVisible: true,
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
    showPrivacyPolicy() {
      this.isPrivacyPolicyVisible = true;
    },
    closePrivacyPolicy() {
      this.isPrivacyPolicyVisible = false;
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
  list-style-type: none; /* Remove the default bullet point */
}

ul.custom-bullet li::before {
  content: "✔ "; /* Add tick mark before each list item */
  color: green; /* Change color of tick mark */
  font-weight: bold; /* Make the tick mark bold */
}
@media (max-width: 767px) {
  .header-logo {
    display: none;
  }
}
</style>
