<template>
  <section>
    <div class="rating-container">
      <h2 v-if="isMobile" @click="toggleRatings">
        Ｒａｔｉｎｇｓ ⭐ {{ showRatings ? "🔽" : "🔼" }}
      </h2>
      <h2 v-else>Ｒａｔｉｎｇｓ ⭐</h2>
      <div v-if="showRatings || !isMobile">
      <div v-for="rating in ratingData" :key="rating._id">
        <div class="rating-main-container">
          <div class="rating-stars">
            <h6>{{ getStarRating(rating.rating) }}</h6>
          </div>
          <div class="rating-timestamp">
            <span>{{ formatTimestamp(rating.timestamp) }}</span>
          </div>
        </div>
        <p class="comments">{{ rating.comments }}</p>
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
      ratingData: [],
      showRatings: false,
      isMobile: false,
    };
  },
  mounted() {
    this.fetchRatings();
    this.checkMobile();
    window.addEventListener("resize", this.checkMobile);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.checkMobile);
  },
  methods: {
    async fetchRatings() {
      try {
        const response = await axios.get(
          "http://35.178.4.216:3000/rating" // Changing test url to production url
        );
        this.ratingData = response.data;
      } catch (error) {
        console.error(`An Error occured while fetching the ratings: ${error}`);
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
    getStarRating(rating) {
      const starRating = "⭐".repeat(Math.floor(rating)); // Full stars
      if (rating % 1 !== 0) {
        starRating += "½"; // Half star if there's a remainder
      }
      return starRating;
    },
    toggleRatings() {
      this.showRatings = !this.showRatings;
    },
    checkMobile() {
      this.isMobile = window.innerWidth < 768; 
    },
  },
};
</script>

<style scoped>
.rating-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  text-align: center;
  padding: 1rem;
}
.rating-container > div {
  border-radius: 9px;
  text-align: left;
  padding: 0 0.5rem 1rem 1rem;
  box-shadow: 0px 0px 8px rgba(17, 17, 26, 0.1);
  background-color: white;
}
.rating-container h2 {
  color: #f07812;
  font-weight: bold;
}
.rating-main-container {
  display: flex;
  justify-content: space-between;
}
.rating-timestamp {
  font-size: 0.7rem;
  /* margin: auto 0; */
  padding-top: 0.3rem;
}
.comments {
  font-size: 1rem;
}
</style>