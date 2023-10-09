<template>
  <section>
    <div class="feedback-container">
      <h2 v-if="isMobile" @click="toggleFeedbacks">
        Ｆｅｅｄｂａｃｋｓ 🌻 {{ showFeedbacks ? "🔽" : "🔼" }}
      </h2>
      <h2 v-else>Ｆｅｅｄｂａｃｋｓ 🌻</h2>
      <!--Give letter spacing here -->
      <div v-if="showFeedbacks || !isMobile">
      <div v-for="feedback in feedbacks" :key="feedback._id">
        <div class="feedback-name-container">
          <h3 class="feedback-name">
            <strong>{{ feedback.name }}</strong>
          </h3>
          <div class="feedback-timestamp">
            <span>{{ formatTimestamp(feedback.timestamp) }}</span>
          </div>
        </div>
        <h5 class="feedback-email">{{ feedback.email }}</h5>
        <p class="feedback">{{ feedback.feedback }}</p>
      </div>
     </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      feedbacks: [],
      showFeedbacks: false,
      isMobile: false,
    };
  },
  computed: {},
  mounted() {
    this.getFeedback();
    this.checkMobile();
    window.addEventListener("resize", this.checkMobile);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.checkMobile);
  },
  methods: {
    async getFeedback() {
      try {
        const response = await axios.get(
          "https://agile-smock-worm.cyclic.app/feedbacks" // Changing test url to production url
        );
        this.feedbacks = response.data;
      } catch (error) {
        console.error(`An error occured while fetching the feedback ${error}`);
      }
    },
    formatTimestamp(timestamp) {
      // Create a Date object from the Unix timestamp (multiply by 1000 to convert to milliseconds)
      const date = new Date(timestamp * 1000);
      // Use date methods to format the date and time as needed
      const formattedDate = date.toLocaleDateString();
      const formattedTime = date.toLocaleTimeString();
      // Combine date and time
      return `${formattedDate} ${formattedTime}`;
    },
    toggleFeedbacks() {
      this.showFeedbacks = !this.showFeedbacks;
    },
    checkMobile() {
     this.isMobile = window.innerWidth < 768; 
    },
  },
};
</script>
<style scoped>
.feedback-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  text-align: center;
  padding: 1rem;
}
.feedback-container > div {
  border-radius: 9px;
  text-align: left;
  padding: 0 0.5rem 1rem 1rem;
  box-shadow: 0px 0px 8px rgba(17, 17, 26, 0.1);
  background-color: white;
}
.feedback-container h2 {
  color: #f07812;
  font-weight: bold;
}
.feedback-name-container {
  display: flex;
  justify-content: space-between;
}
.feedback-name {
  font-size: 1.2rem;
}
.feedback-timestamp {
  font-size: 0.7rem;
  /* margin: auto 0; */
  padding-top: 0.3rem;
}
.feedback-email {
  font-size: 0.7rem;
  margin-top: 0;
}
.feedback {
  font-size: 1rem;
}
@media (max-width: 968px) {
  .feedback-name {
    font-size: 1rem;
  }
}
</style>