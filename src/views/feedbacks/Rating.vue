<template>
  <the-disclaimer
    v-show="isVisible"
    @close="close"
    :modalWidth="modalWidth"
    :modalHeight="modalHeight"
  >
    <template v-slot:header>
      <h2>Rate Us</h2>
    </template>
    <template #body>
      <div v-if="!thankYouMessage" class="rating-container">
        <!-- <br /> -->

        <h5>How would you rate this product?</h5>
        <!-- <br /> -->

        <div class="rating">
          <img
            v-for="(star, index) in 5"
            :key="index"
            :src="
              index < currentRating ? filledStarImageUrl : regularStarImageUrl
            "
            @click="updateRating(index + 1)"
            style="cursor: pointer"
          />
        </div>
        <br />
        <!-- <br /> -->

        <textarea
          placeholder="Anything you would like to add...."
          ref="feedbackTextarea"
        ></textarea>
        <!-- <br /> -->
        <!-- <br /> -->
        <button class="submit-rating" @click="submitRating">Submit</button>
      </div>
      <div class="thank-you-msg" v-else>
        <br />
        <br />
        <p>Thank you for rating AskLlama! 🌻</p>
        <br />
        <br />
        <img class="logo-llama" src="../../assets/llama-lgo.png" />
      </div>
    </template>
  </the-disclaimer>
</template>

<script>
import axios from "axios";
import TheDisclaimer from "../legals/TheDisclaimer.vue";
import star from "../../assets/star.png";
import star1 from "../../assets/star (1).png";

export default {
  components: {
    TheDisclaimer,
  },

  data() {
    return {
      isVisible: false,
      currentRating: 0,
      thankYouMessage: false,
      modalWidth: "26%",
      modalHeight: "50vh",
      regularStarImageUrl: star,
      filledStarImageUrl: star1,
    };
  },

  methods: {
    show() {
      this.isVisible = true;
    },
    close() {
      this.isVisible = false;
    },
    updateRating(rating) {
      this.currentRating = rating;
    },

    async submitRating() {
      if (this.currentRating === 0) {
        alert("Please select at least one star before submitting your rating.");
        return;
      }

      const feedbackText = this.$refs.feedbackTextarea.value.trim();
      if (feedbackText === "") {
        alert("Please provide your feedback before submitting your rating.");
        return;
      }

      // Prepare the data to be sent in the POST request
      const postData = {
        rating: this.currentRating,
        comments: feedbackText,
      };

      try {
        // Make a POST request to your backend API
        const response = await axios.post(
          "https://agile-smock-worm.cyclic.app/rating/post", // Changing test url to production url
          postData
        );

        // Check if the POST request was successful
        if (response.status === 200) {
          this.thankYouMessage = true;
        } else {
          alert("Failed to submit your rating. Please try again later.");
        }
      } catch (error) {
        console.error("Error submitting rating:", error);
        alert(
          "An error occurred while submitting your rating. Please try again later."
        );
      }
    },
  },
};
</script>

<style scoped>
.rating-container {
  text-align: center;
  margin-top: 2rem;
}

.rating {
  text-align: center;
  display: flex;
  justify-content: center;
  font-size: 3rem;
  margin-top: 1rem;
}
.rating > img {
  width: 40px;
  cursor: pointer;
}

textarea {
  background-color: white;
  padding: 10px;
  width: 80%;
  height: 100px;
  text-decoration: none;
  border: none;
  box-shadow: rgba(17, 17, 26, 0.05) 0px 4px 16px,
    rgba(17, 17, 26, 0.05) 0px 8px 32px;

  border-radius: 9px;
  margin-top: 1.5rem;
}
.submit-rating {
  margin: 2rem auto;
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

.submit-rating:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
  letter-spacing: 0.3em;
}
.thank-you-msg {
  text-align: center;
  font-size: 1.5rem;
}
.logo-llama {
  margin: auto;
  width: 70px;
}
@media (max-width: 767px) {
  .rating-container {
    margin-top: 0;
  }
  .rating {
    margin-top: 0;
  }
  textarea {
    width: 95%;
    margin-top: 0;
  }
  .submit-rating {
    margin-top: 2rem;
  }
  .thank-you-msg {
    text-align: center;
    font-size: 1.4rem;
  }
}

.alert-message {
  font-size: 1.2rem;
  margin: 0;
  color: #333;
}

.alert-button {
  color: #fff;
  background-color: #f09819;
  border-radius: 5px;
  padding: 8px 20px;
  font-size: 1.2rem;
  cursor: pointer;
}

.alert-button:hover {
  background-color: #ff512f;
}
</style>
