<template>
  <div class="selected-masters-container">
    <h2 class="selected-masters-header">Selected Masters</h2>
    <div class="selected-masters-list">
      <div
        class="selected-master"
        v-for="master in selectedMasters"
        :key="master.name"
      >
        <img :src="master.image" :alt="master.name" class="master-image" />
        <p class="master-name">{{ master.name }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
const selectedMasters =
  JSON.parse(localStorage.getItem("selectedMasters")) || [];
</script>

<style scoped>
.selected-masters-container {
  padding: 20px;
}

.selected-masters-header {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #f07812;
}

.selected-masters-list {
  display: flex;
  flex-wrap: wrap;
}

.selected-master {
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
</style>
