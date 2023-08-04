<template>
  <div class="selected-masters-container">
    <div v-if="selectedMasters.length === 0" class="select-masters-message">
      Select the masters
    </div>
    <div v-else class="selected-masters-list">
      <div
        class="selected-master"
        v-for="master in selectedMasters"
        :key="master.name"
      >
        <p class="remove-master" @click="removeMaster(master)">×</p>

        <img :src="master.image" :alt="master.name" class="master-image" />
        <p class="master-name">{{ master.name }}</p>
      </div>
      <a href="/master" class="plus-icon">
        <img src="../assets/plus.png" />
      </a>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const selectedMasters = ref(
  JSON.parse(localStorage.getItem("selectedMasters")) || []
);

const removeMaster = (masterToRemove) => {
  const index = selectedMasters.value.findIndex(
    (master) => master.name === masterToRemove.name
  );
  if (index !== -1) {
    selectedMasters.value.splice(index, 1);
  }
};

watch(selectedMasters, (newValue) => {
  localStorage.setItem("selectedMasters", JSON.stringify(newValue));
});

</script>

<style scoped>
.selected-masters-container {
  padding: 20px;
}

.remove-master {
  font-size: 20px;
  /* border: 1px solid red; */
  margin-left: 30px;
  opacity: 0;
  pointer-events: none;
}

.selected-master:hover .remove-master {
  opacity: 1;
  pointer-events: auto;
}

.selected-masters-header {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #f07812;
}

.selected-masters-list {
  display: flex;
  overflow-x: auto;
  padding: 10px;
}

.selected-master {
  width: 120px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-right: 20px;
  /* border: 1px solid red; */
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

.plus-icon {
  display: flex;
  justify-content: center; /* Center the image horizontally */
  align-items: center; /* Center the image vertically */
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  background-color: white;
}

.plus-icon > img {
  width: 20px;
  height: 20px;
}
</style>
