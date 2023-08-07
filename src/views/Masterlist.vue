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
  },
  mounted() {
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
  box-shadow: rgb(44, 55, 67) 0px 20px 30px -10px;
  transform: scale(1.2);
  border: 2px solid #f07812;
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
  flex-wrap: wrap;
  padding: 10px;
}

.back-icon > img {
  width: 100%;
  width: 30px;
  height: 30px;
  cursor: pointer;
}
.master {
  text-align: center;
  width: 100px;
  margin: 10px 20px;
}

.master-image {
  width: 50px;
  height: 50px;
  cursor: pointer;

  border-radius: 50%;
}

.master-name {
  margin-top: 10px;
  font-size: 14px;
  text-align: center;
}

.ellipsis {
}
.master-header-name {
  padding-left: 20px;
  color: #f07812;
  font-family: "Trebuchet MS", sans-serif;
}

@media (max-width: 768px) {
  .masters-container {
    display: flex;
    flex-wrap: wrap;
    padding-left: 12vw;
  }
}
</style>
