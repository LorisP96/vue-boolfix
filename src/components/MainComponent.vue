<template>
  <main>
    <div class="card-container">
      <div class="card" v-for="card, index in arrayResult" :key="index">
        <div class="info-card">
          <h2>{{card.title}}</h2>
          <div>{{card.original_title}}</div>
          <div>{{card.original_language}}</div>
          <div class="vote">
            <span>{{card.vote_average}}</span>
            <span>{{card.vote_count}}</span>
          </div>
        </div>
        <img :src="'https://image.tmdb.org/t/p/w342' + card.poster_path" alt="">
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
    width: calc((100% / 6) - 10px);
    margin: 5px;
    aspect-ratio: 3/4;
    position: relative;
    img {
      display: block;
      width: 100%;
      aspect-ratio: 3/4;
      object-position: center;
    }
    .info-card {
      color: white;
      position: absolute;
      top: 0;
      right: 0;
      left: 0;
      bottom: 0;
      opacity: 0;
      padding: 20px;
      .vote {
        display: flex;
      }
    }
    &:hover .info-card {
      opacity: 1;
      background-color: rgba($color: black, $alpha: 0.5);
    }
  }
}
</style>