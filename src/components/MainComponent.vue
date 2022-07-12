<template>
  <main>
    <div class="card-container">
      <div class="card" v-for="card, index in arrayResult" :key="index">
        <h3>{{card.title}}</h3>
        <div>{{card.original_title}}</div>
        <div>{{card.original_language}}</div>
        <div class="vote">
          <span>{{card.vote_average}}</span>
          <span>{{card.vote_count}}</span>
        </div>
      </div>
    </div>
  </main>
</template>

<script>

export default {
  name: 'MainComponent',
  props: {
    arrayResult: Array,
  },
  data() {
    return {
    }
  },
  methods: {
    
  },
}
</script>

<style lang="scss" scoped>
.card-container {
  display: flex;
  flex-wrap: wrap;
  width: calc(100% - 80px);
  margin: 0 auto;
  padding-top: 40px;
  .card {
    width: calc(100% / 6);
    height: 300px;
    padding: 20px;
    border: 1px solid pink;
    .vote {
      display: flex;
    }
  }
}
</style>