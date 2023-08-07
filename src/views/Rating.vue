<template>
  <the-disclaimer v-show="isVisible" @close="close">
    <template v-slot:header>
      <h2>Rate Us</h2>
    </template>
    <template #body>
      <div v-if="!thankYouMessage" class="rating-container">
        <h5>How would you rate this product?</h5>
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
        <textarea placeholder="Anything you would like to add...."></textarea>
        <br />
        <br />
        <button class="submit-rating" @click="submitRating">Submit</button>
      </div>
      <div class="thank-you-msg" v-else>
        <h2>Thank you for rating AskLlama! 🌻</h2>
        <br />
        <br />
        <img class="logo-llama" src="../assets/llama-lgo.png" />
      </div>
    </template>
  </the-disclaimer>
</template>

<script>
import TheDisclaimer from "./TheDisclaimer.vue";
export default {
  components: {
    TheDisclaimer,
  },

  data() {
    return {
      isVisible: false,
      currentRating: 0,
      thankYouMessage: false,
      regularStarImageUrl:
        "https://github.com/Piryanshu88/Mind_Maze/assets/97978681/d8cd7554-0f34-4882-9952-83b2c394e3b9",
      filledStarImageUrl:
        "https://github.com/Piryanshu88/Mind_Maze/assets/97978681/369e85a8-a086-47db-83d0-bd0edb7ef562",
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
    submitRating() {
      if (this.currentRating === 0) {
        alert("Please select at least one star before submitting your rating.");
        return;
      }

      const feedbackText = document
        .querySelector(".rating-container textarea")
        .value.trim();
      if (feedbackText === "") {
        alert("Please provide your feedback before submitting your rating.");
        return;
      }

      this.thankYouMessage = true;
    },
  },
};
</script>

<style scoped>
.rating-container {
  text-align: center;
}

.rating {
  text-align: center;
  display: flex;
  justify-content: center;
  font-size: 3rem;
  /* border: 1px solid red; */
}
.rating > img {
  width: 40px;
  cursor: pointer;
}

textarea {
  background-color: white;
  padding: 10px;
  width: 400px;
  height: 100px;
  text-decoration: none;
  border: none;
  box-shadow: rgba(17, 17, 26, 0.05) 0px 4px 16px,
    rgba(17, 17, 26, 0.05) 0px 8px 32px;

  border-radius: 30px;
}
.submit-rating {
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

.submit-rating:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
  letter-spacing: 0.3em;
}
.thank-you-msg {
  text-align: center;
}
.logo-llama {
  margin: auto;
  width: 70px;
}
@media (max-width: 767px) {
  textarea {
    width: 95%;
  }
}
</style>
