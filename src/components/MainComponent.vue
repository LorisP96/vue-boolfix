<template>
  <main>
    <div class="card-container">
      <div class="card" v-for="card, index in arrayFilmResult" :key="'a' + index">
        <div class="info-card">
          <h2>{{card.title}}</h2>
          <img :src="'https://countryflagsapi.com/svg/' + fixFlag(card.original_language)" alt="">
          <div class="vote">
            <span>media voti: {{card.vote_average}}</span>
            <span>numero di recensioni: {{card.vote_count}}</span>
          </div>
          <div class="original-text">{{card.original_title}}</div>
        </div>
        <img :src="'https://image.tmdb.org/t/p/w342' + card.poster_path" :alt="card.title">
      </div>
      <div class="card" v-for="cardtv, index in arrayTvResult" :key="'b' + index">
        <div class="info-card">
          <h2>{{cardtv.name}}</h2>
          <img :src="'https://countryflagsapi.com/svg/' + fixFlag(cardtv.original_language)" alt="">
          <div class="vote">
            <span>media voti: {{cardtv.vote_average}}</span>
            <span>numero di recensioni: {{cardtv.vote_count}}</span>
          </div>
          <div class="original-text">{{cardtv.original_name}}</div>
        </div>
        <img :src="'https://image.tmdb.org/t/p/w342' + cardtv.poster_path" :alt="cardtv.name">
      </div>
    </div>
  </main>
</template>

<script>

export default {
  name: 'MainComponent',
  props: {
    arrayFilmResult: Array,
    arrayTvResult: Array,
  },
  methods: {
    fixFlag(flag) {
      if(flag == 'en'){
        return flag = "gb";
      } else if(flag == 'ja'){
        return flag = "jp";       
      } else if(flag == 'hi'){
        return flag = "in";      
      } else if(flag == 'cs'){
        return flag = "cz";       
      } else if(flag == 'ko'){
        return flag = "kr";       
      } else if(flag == 'sv'){
        return flag = "ch";       
      } return flag
    }
  }
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
    aspect-ratio: 2/3;
    position: relative;

    img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
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
      overflow-y: auto;
      .original-text {
        font-size: 14px;
        margin: 10px 0;
      }

      img {
        width: 30px;
        aspect-ratio: 1/1;
        border-radius: 50%;
        height: auto;
        margin: 10px 0;
        position: absolute;
        bottom: 20px;
        right: 20px;
        border: 3px solid white;
      }

      .vote {
        font-size: 10px;
        display: flex;
        justify-content: space-between;
      }
    }
    &:hover .info-card {
      opacity: 1;
      background-color: rgba($color: black, $alpha: 0.5);
    }
  }
}
</style>