<template>
  <the-disclaimer v-show="isVisible" @close="close">
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
          As much as we love our AskLlama characters, they are not the originals
          but only representations. Don't worry though, they still have all the
          personality and charm of the original Masters 😎
        </li>
        <br />
        <li>
          AskLlama responses are for informational purposes only and should not
          be treated as sage advice. So, if you're looking to quit your job and
          become a llama herder because of something we said, maybe double check
          with an actual professional first.
        </li>
        <br />
        <li>
          AskLlama may occasionally provide inaccurate information or use humour
          (our best quality obviously) that may not be everyone’s cup of tea.
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
    };
  },
  methods: {
    show() {
      this.isVisible = true;
    },
    close() {
      this.isVisible = false;
    },
  },
};
</script>

<style scoped>
/* Add necessary styles here */
</style>
