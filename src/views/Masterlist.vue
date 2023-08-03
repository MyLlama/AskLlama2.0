<template>
  <div>
    <h2 class="master-header-name">{{ title }}</h2>
    <div class="masters-container">
      <div
        class="master"
        v-for="master in masters"
        :key="master.name"
        @click="toggleMasterSelection(master)"
        :class="{ 'selected-master': master.selected }"
      >
        <img :src="master.image" :alt="master.name" class="master-image" />
        <p class="master-name" :class="{ ellipsis: master.name.length > 8 }">
          {{ master.name }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    masters: Array,
    selectedMasters: Array,
  },
  methods: {
    toggleMasterSelection(master) {
      master.selected = !master.selected;
      this.saveSelectedMasters();
    },
    saveSelectedMasters() {
      const allSelectedMasters = [].concat(
        ...this.$parent.prophets.filter((master) => master.selected),
        ...this.$parent.contemporary.filter((master) => master.selected),
        ...this.$parent.mystics.filter((master) => master.selected),
        ...this.$parent.Philosophers.filter((master) => master.selected),
        ...this.$parent.Psycologists.filter((master) => master.selected),
        ...this.$parent.fictional.filter((master) => master.selected)
      );
      this.$emit("selectedMastersChange", allSelectedMasters);
    },
  },
  created() {
    const selectedMasters =
      JSON.parse(localStorage.getItem("selectedMasters")) || [];
    this.masters.forEach((master) => {
      master.selected = selectedMasters.some(
        (selectedMaster) => selectedMaster.name === master.name
      );
    });
    this.saveSelectedMasters();
  },
};
</script>

<style scoped>
.selected-master .master-image {
  border: 2px solid red;
}
.master-header {
  padding: 10px;
  display: flex;
  background-color: #f07812;
  color: white;
  font-family: "Trebuchet MS", sans-serif;
}
.master-header h1 {
  margin: auto;
}
.masters-container {
  display: flex;
  overflow-x: auto;
  padding: 10px;
}

.back-icon > img {
  width: 100%;
  width: 30px;
  height: 30px;
}
.master {
  width: 120px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-right: 20px;
}

.master-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

.master-name {
  margin-top: 10px;
  font-size: 14px;
  text-align: center;
}

.ellipsis {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 5rem;
}
.master-header-name {
  padding-left: 20px;
  color: #f07812;
  font-family: "Trebuchet MS", sans-serif;
}
</style>
