<template>
    <the-disclaimer v-show="isVisible" @close="closeDisclaimer">
      <template v-slot:header>
        <h2>{{ header }}</h2>
      </template>
      <template #body>
        {{ content }}
      </template>
    </the-disclaimer>
  </template>
  
  <script>
  import TheDisclaimer from "./TheDisclaimer.vue";
  
  export default {
    components: {
      TheDisclaimer,
    },
    props: {
      isVisible: Boolean,
      header: String,
      content: String,
    },
    methods: {
      closeDisclaimer() {
        this.$emit("close");
      },
    },
  };
  </script>
  