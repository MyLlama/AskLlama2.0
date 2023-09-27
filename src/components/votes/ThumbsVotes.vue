<template>
  <section>
    <div class="vote-main-container">
      <h2>Ｔｈｕｍｂｖｏｔｅｓ</h2>

      <div class="vote-columns">
        <vote-list :votes="upVotes" title="Ｕｐ Ｖｏｔｅｓ 👍"></vote-list>
        <vote-list :votes="downVotes" title="Ｄｏｗｎ Ｖｏｔｅｓ 👎"></vote-list>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
import VoteList from "./VoteList.vue";

export default {
  components: {
    VoteList,
  },
  data() {
    return {
      upVotes: [],
      downVotes: [],
    };
  },
  mounted() {
    this.getThumbVotes();
  },
  methods: {
    async getThumbVotes() {
      try {
        const response = await axios.get(
          "https://agile-smock-worm.cyclic.app/thumbvote"
        );
        // Filter upvotes and downvotes based on some criteria
        // console.log(response.data)
        this.upVotes = response.data.filter((item) => item.vote === true);
        this.downVotes = response.data.filter((item) => item.vote === false);
        // console.log(this.upVotes);
      } catch (error) {
        console.error(
          `An error occured while fetching the thumbvotes: ${error}`
        );
      }
    },
  },
};
</script>

<style scoped>
.vote-main-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  text-align: center;
  padding: 1rem;
}

.vote-main-container > div {
  border-radius: 9px;
  text-align: left;
  /* padding: 0 0.5rem 1rem 1rem; */
  background-color: transparent;
  /* box-shadow: 0px 0px 16px rgba(17, 17, 26, 0.25); */
}

.vote-main-container h2 {
  color: #f07812;
  font-weight: bold;  
}

.vote-columns {
  display: flex;
  justify-content: space-between;
}

@media (max-width: 968px) {
  .vote-columns {
    display: flex;
    flex-direction: column;
  }
}
</style>
