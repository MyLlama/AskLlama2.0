<template>
  <section>
    <div class="rating-container">
      <h2>Ｒａｔｉｎｇｓ ⭐</h2>
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
  </section>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      ratingData: [],
    };
  },
  mounted() {
    this.fetchRatings();
  },
  methods: {
    async fetchRatings() {
      try {
        const response = await axios.get(
          "https://agile-smock-worm.cyclic.app/rating"
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
