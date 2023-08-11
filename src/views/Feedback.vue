<template>
  <the-disclaimer
    v-show="isVisible"
    @close="close"
    :modalWidth="modalWidth"
    :modalHeight="modalHeight"
  >
    <template v-slot:header>
      <h2>Feedback</h2>
    </template>
    <template #body>
      <div class="feedback-container" v-if="!thankYouMessage">
        <label>Name</label>
        <input ref="nameInput" placeholder="Name" />
        <label>Email</label>
        <input ref="emailInput" placeholder="Email" />
        <label>Feedback</label>
        <textarea
          ref="feedbackTextarea"
          class="feedback-textarea"
          placeholder="Share your thoughts"
        ></textarea>
        <button class="submit-rating" @click="submitFeedback">Submit</button>
      </div>
      <div class="thank-you-msg" v-else>
        <br />
        <br />
        <p>Thank you for Your Valuable Feedback! 🌻</p>
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
      thankYouMessage: false,
      modalWidth: "26%",
      modalHeight: "60vh",
    };
  },
  methods: {
    show() {
      this.isVisible = true;
    },
    close() {
      this.isVisible = false;
    },
    submitFeedback() {
      const name = this.$refs.nameInput.value;
      const email = this.$refs.emailInput.value;
      const feedback = this.$refs.feedbackTextarea.value;
      if (!name || !email || !feedback) {
        alert("Please fill in all the required fields!");
        return;
      }
      this.thankYouMessage = true;
    },
  },
};
</script>

<style scoped>
.feedback-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin: auto;
  width: 99%;
  padding: 10px;
}
input {
  padding: 10px;
  background-color: white;
  border: none;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 5px 15px 0px;
  border-radius: 10px;
}
.feedback-textarea {
  background-color: white;
  padding: 10px;
  width: 100%;
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
.logo-llama {
  margin: auto;
  width: 70px;
}
.thank-you-msg {
  text-align: center;
  font-size: 1.5rem;
}
@media (max-width: 767px) {
  textarea {
    width: 95%;
  }
  .feedback-container {
    width: 99%;
  }
  .thank-you-msg {
    text-align: center;
    font-size: 1.4rem;
  }
}
</style>
