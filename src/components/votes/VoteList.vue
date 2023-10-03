<template>
  <div class="vote-column">
    <h4>{{ title }}</h4>
    <div v-for="vote in votes" :key="vote._id" class="container">
      <!-- <div class="vote-container"> -->
      <div class="vote-timestamp">
        <span>{{ formatTimestamp(vote.timestamp) }}</span>
      </div>
      <!-- </div> -->
      <div class="master">
        <span class="label">Master:</span>
        <span class="content">{{ vote.master }}</span>
      </div>
      <div class="master-answer">
        <span>
          <span class="label">Answer:</span>
          <span class="content">{{ vote.answer }}</span>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    votes: Array, // An array of votes
    title: String, // Title for the list
  },
  methods: {
    getVoteText(vote) {
      return vote ? "👍" : "👎";
    },
    formatTimestamp(timestamp) {
      // Create a Date object from the Unix timestamp (multiply by 1000 to convert to milliseconds)
      const date = new Date(timestamp * 1000);

      // Use date methods to format the date and time as needed
      const formattedDate = date.toLocaleDateString();
      const formattedTime = date.toLocaleTimeString();

      // Combine date and time
      return `${formattedDate} ${formattedTime}`;
    },
  },
};
</script>

<style scoped>
.vote-column {
  flex: 1;
  padding: 0.5rem;
}
.vote-column h4 {
  text-align: center;
  margin-bottom: 1rem;
  color: #f07812;
  font-weight: 900;
}

.container {
  border-radius: 9px;
  margin-bottom: 1rem;
  padding: 0 1rem 1rem;
  box-shadow: 0px 0px 8px rgba(17, 17, 26, 0.1);
  background-color: white;
}

.vote-container {
  display: flex;
  justify-content: space-between;
}

.vote-timestamp {
  padding-top: 0.3rem;
  font-size: 0.7rem;
  text-align: right;
}

.master,
.master-answer {
  display: flex;
  align-items: center;
}

.label {
  font-weight: bold;
  margin-right: 0.5rem;
}

.content {
  margin: 0;
}
</style>
