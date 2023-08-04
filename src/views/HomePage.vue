<template>
  <AppHeader />
  <SelectedMasters />
</template>

<script>

import AppHeader from "../views/Header.vue";
import SelectedMasters from "../views/SelectedMasters.vue";


export default {
  components: {
    AppHeader,
    SelectedMasters,
  },

  data() {
    return {
      showMenu: false,
    };
  },
  methods: {
    toggleMenu() {
      this.showMenu = !this.showMenu;
    },
  },
};
</script>

<style scoped></style>
