<template>
  <div id="admin-container">
    <div class="header">Askllama Admin Page</div>
    <div class="feedback-container">
      <div class="feedback">
        <the-testimonials></the-testimonials>

        <the-ratings></the-ratings>
      </div>
      <div class="thumb-votes">
        <thumbs-votes></thumbs-votes>
      </div>
    </div>
  </div>
</template>

<script>
import TheTestimonials from "../components/feedbacks/TheTestimonials.vue";
import TheRatings from "../components/feedbacks/TheRatings.vue";
import ThumbsVotes from "../components/votes/ThumbsVotes.vue";

export default {
  components: {
    TheTestimonials,
    TheRatings,
    ThumbsVotes,
  },
};
</script>

<style scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.header {
  text-align: center;
  padding: 2vh;
  font-weight: bold;
  font-size: 2rem;
  color: white;
  background-color: #f07812;
}
#admin-container {
  font-family: inherit;
  font-weight: 400;
  color: #333;
  /* background-color: #dceffb; */
  background-color: #fcf7ee;
  /* background-image: linear-gradient(to top left, #dceffb 0%, #f07812 100%); */
}

.feedback-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  
}
.feedback {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  position: relative;
  /* height: 100vh; */
  background-color: #FCF7EE;
  backdrop-filter: blur(200px);
  filter: blur();
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
  border-radius: 9px;
  overflow: hidden;
  margin: 1rem;
  /* padding: 2rem; */
}

.thumb-votes {
  position: relative;
  height: 100vh;
  background-color: #FCF7EE;
  backdrop-filter: blur(200px);
  filter: blur();
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
  border-radius: 9px;
  margin: 1rem;
  /* padding: 2rem; */
}

@media (max-width: 968px) {
  .feedback-container {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  
}
  .feedback {
    grid-template-columns: repeat(2, 1fr);
  }

  .header {
 
  font-size: 1.6rem;
  
}
}
@media (max-width: 480px) {
  .feedback {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
