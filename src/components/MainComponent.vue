<template>
  <main>

    <h2 class="categories">Film</h2>
    <div class="card-container">
      
      <div class="card" v-for="card, index in arrayFilmResult" :key="'a' + index">
        <div class="info-card">
          <h3>{{card.title}}</h3>
          <img :src="'https://countryflagsapi.com/svg/' + fixFlag(card.original_language)" alt="">
          <div class="vote">
            <span class="gold" v-for="star, index in fixStar(card.vote_average)" :key="'c' + index"><i class="fa-solid fa-star"></i></span>
            <span v-for="star, index in (5 - fixStar(card.vote_average))" :key="'d' + index"><i class="fa-regular fa-star"></i></span>
            <div>numero di recensioni: {{card.vote_count}}</div>
          </div>
          <div class="original-text">{{card.overview}}</div>
        </div>
        <img v-if="card.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342' + card.poster_path" :alt="card.title">
        <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRzOvaNmJGJ0BCxEpCqAVKnhVAE8T6IPNODaw&usqp=CAU" :alt="card.title">
      </div>
    </div>

    <h2 class="categories">Serie TV</h2>
    <div class="card-container">
      
      <div class="card" v-for="cardtv, index in arrayTvResult" :key="'b' + index"> 
        <div class="info-card">
          <h3>{{cardtv.name}}</h3>
          <img :src="'https://countryflagsapi.com/svg/' + fixFlag(cardtv.original_language)" alt="">
          <div class="vote">
            <span class="gold" v-for="index in fixStar(cardtv.vote_average)" :key="'c' + index"><i class="fa-solid fa-star"></i></span>
            <span v-for="index in (5 - fixStar(cardtv.vote_average))" :key="'d' + index"><i class="fa-regular fa-star"></i></span>
            <div>numero di recensioni: {{cardtv.vote_count}}</div>
          </div>
          <div class="original-text">{{cardtv.overview}}</div>
        </div>
        <img v-if="cardtv.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342' + cardtv.poster_path" :alt="cardtv.name">
        <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRzOvaNmJGJ0BCxEpCqAVKnhVAE8T6IPNODaw&usqp=CAU" :alt="cardtv.name">
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
  data() {
    return {
    }
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
      } else if(flag == 'fa'){
        return flag = "ir";
      } else if(flag == 'sv'){
        return flag = "ch";       
      } return flag
    },
    fixStar(star) {
      return Math.round(star / 2);
    }
  },

}

</script>

<style lang="scss" scoped>
main {
  height: calc(100vh - 70px);
  .categories {
    color: white;
    padding: 15px 40px;
    font-size: 28px;
  }
  .card-container {
    display: flex;
    width: calc(100% - 80px);
    margin: auto;
    height: calc(50% - 67px);
    overflow-x: auto;
    margin-bottom: 5px;

    /* total width */
    &::-webkit-scrollbar {
      background-color: #434343;
      width: 16px;
      height: 8px;
    }

    /* background of the scrollbar except button or resizer */
    &::-webkit-scrollbar-track {
      background-color:#2e2e2e81;
    }

    /* scrollbar itself */
    &::-webkit-scrollbar-thumb {
      background-color: #babac0;
      border-radius: 16px;
    }

    /* set button(top and bottom of the scrollbar) */
    &::-webkit-scrollbar-button {
        display:none;
    }

    .card {
      aspect-ratio: 2/3;
      margin: 3px;
      position: relative;
      flex-shrink: 0;

      img {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
      }

      .info-card {
        color: white;
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        opacity: 0;
        padding: 20px 30px;
        overflow-y: auto;

        &::-webkit-scrollbar {
          background-color: #434343;
          width: 5px;
          height: 5px;
        }

        &::-webkit-scrollbar-track {
          background-color:#2e2e2e81;
        }

        &::-webkit-scrollbar-thumb {
          background-color: #babac0;
          border-radius: 16px;
        }

        &::-webkit-scrollbar-button {
          display:none;
        }

        .original-text {
          font-size: 14px;
          margin: 10px 0;
        }

        img {
          width: 25px;
          aspect-ratio: 1/1;
          border-radius: 50%;
          height: auto;
          margin: 10px 0;
          position: absolute;
          top: 0;
          right: 5px;
          border: 2px solid white;
        }

        .vote {
          font-size: 13px;
          line-height: 20px;
          padding-top: 8px;

          .gold {
            color: goldenrod;
          }

          span {
            font-size: 16px;
          }
        }
      }
      &:hover .info-card {
        opacity: 1;
        background-color: rgba($color: black, $alpha: 0.5);
      }
    }
  }
}
</style>