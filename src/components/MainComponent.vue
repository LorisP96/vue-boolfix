<template>
  <main>
    <!-- FILM -->
    <h2 class="categories" v-if="arrayFilmResult.length !== 0">Film</h2>

    <div class="card-container">
      <!-- CARD -->
      <div class="card" v-for="card, index in arrayFilmResult" :key="'a' + index">
        <!-- elementi in hover di ogni singola card -->
        <div class="info-card" @mouseenter="getActorArray(card.id)">
          <!-- titolo -->
          <h3>{{card.title}}</h3>
          <!-- lingua -->
          <img :src="'https://countryflagsapi.com/svg/' + fixFlag(card.original_language)" alt="">
          <!-- recensioni -->
          <div class="vote">
            <span class="gold" v-for="star, index in fixStar(card.vote_average)" :key="'c' + index"><i class="fa-solid fa-star"></i></span>
            <span v-for="index in (5 - fixStar(card.vote_average))" :key="'d' + index"><i class="fa-regular fa-star"></i></span>
            <div>numero di recensioni: {{card.vote_count}}</div>
          </div>
          <!-- descrizione film o serie -->
          <div class="overview-text">{{card.overview}}</div>
          <div v-if="card.title !== card.original_title" class="original">{{card.original_title}}</div>
          <!-- lista attori -->
          <div v-if="actorArray.length !== 0" class="actors-list">
            <span v-for="element, index in actorArray" :key="'e' + index">{{element}}, </span>
            <span> ecc...</span>
          </div>
        </div>
        <!-- poster -->
        <img v-if="card.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342' + card.poster_path" :alt="card.title">
        <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRzOvaNmJGJ0BCxEpCqAVKnhVAE8T6IPNODaw&usqp=CAU" :alt="card.title">
      </div>
    </div>

    <!-- SERIE TV -->
    <h2 class="categories" v-if="arrayTvResult.length !== 0">Serie TV</h2>

    <div class="card-container">
      <!-- CARD -->
      <div class="card" v-for="cardtv, index in arrayTvResult" :key="'b' + index"> 
        <!-- elementi in hover di ogni singola card -->
        <div class="info-card" @mouseenter="getTvActorArray(cardtv.id)">
          <!-- titolo -->
          <h3>{{cardtv.name}}</h3>
          <!-- lingua -->
          <img :src="'https://countryflagsapi.com/svg/' + fixFlag(cardtv.original_language)" alt="">
          <!-- recensioni -->
          <div class="vote">
            <span class="gold" v-for="index in fixStar(cardtv.vote_average)" :key="'c' + index"><i class="fa-solid fa-star"></i></span>
            <span v-for="index in (5 - fixStar(cardtv.vote_average))" :key="'d' + index"><i class="fa-regular fa-star"></i></span>
            <div>numero di recensioni: {{cardtv.vote_count}}</div>
          </div>
          <!-- descrizione film o serie -->
          <div class="overview-text">{{cardtv.overview}}</div>
          <div v-if="cardtv.name !== cardtv.original_name" class="original">{{cardtv.original_name}}</div>
          <!-- lista attori -->
          <div v-if="actorTvArray.length !== 0" class="actors-list">
            <span v-for="element, index in actorTvArray" :key="'e' + index">{{element}}, </span>
            <span> ecc...</span>
          </div>
        </div>
        <!-- poster -->
        <img v-if="cardtv.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342' + cardtv.poster_path" :alt="cardtv.name">
        <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRzOvaNmJGJ0BCxEpCqAVKnhVAE8T6IPNODaw&usqp=CAU" :alt="cardtv.name">
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios'

export default {
  name: 'MainComponent',
  props: {
    arrayFilmResult: Array,
    arrayTvResult: Array,
  },
  data() {
    return {
      actorApiStart: 'https://api.themoviedb.org/3/movie/',
      actorTvApiStart: 'https://api.themoviedb.org/3/tv/',
      actorApiEnd: '/credits?api_key=cd6f03323d12eed84d94ab2ac42d791e&language=it-IT',
      actorApi: '',
      actorTvApi: '',
      actorArray: [],
      actorTvArray: [],
    }
  },
  methods: {
    // funzione per sostituire le iniziali della lingua [cerca in template (commenti) 'lingua']
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
    // funzione per trasformare le valutazioni da 1/10 a 1/5 [cerca in template (commenti) 'recensioni']
    fixStar(star) {
      return Math.round(star / 2);
    },
    // funzione per ottenere i nomi dei primi 5 attori, da un'altra API (vedi data)  
    // [CALL cerca in template (commenti) 'elementi in hover di ogni singola card']
    getActorArray(filmid) {
      this.actorApi = this.actorApiStart + filmid + this.actorApiEnd;
      this.actorArray = [];
      axios.get(this.actorApi)
      .then(response => {

        if(response.data.cast.length >= 5 ) {
          for (let i = 0; i < 5; i++) {
          
            this.actorArray.push(response.data.cast[i].name);
          }
        } else if (response.data.cast.length <= 4){
          for (let i = 0; i < response.data.cast.length; i++) {
          
            this.actorArray.push(response.data.cast[i].name);
          }
        } else {
          this.actorArray.push('cast empty')
        }
        // [PRINT cerca in template (commenti) 'lista attori']
        return this.actorArray;
      })
    },
    // stesso procedimento per le serie tv
    getTvActorArray(tvid) {
      this.actorTvApi = this.actorTvApiStart + tvid + this.actorApiEnd;
      this.actorTvArray = [];
      axios.get(this.actorTvApi)
      .then(response => {

        if(response.data.cast.length >= 5 ) {
          for (let i = 0; i < 5; i++) {
          
            this.actorTvArray.push(response.data.cast[i].name);
          }
        } else if (response.data.cast.length <= 4){
          for (let i = 0; i < response.data.cast.length; i++) {
          
            this.actorTvArray.push(response.data.cast[i].name);
          }
        } else {
          this.actorTvArray.push('cast empty')
        }
        // [PRINT cerca in template (commenti) 'lista attori']
        return this.actorTvArray;
      })
    }
  }
}

</script>

<style lang="scss" scoped>
@import '../assets/scss/variables.scss';
main {
  margin-block: 70px;
  .categories {
    color: $text-color;
    padding-top: 60px;
    padding-inline: 40px;
    font-size: 32px;
  }
  .card-container {
    display: flex;
    width: calc(100% - 70px);
    margin: 0 auto;
    overflow-x: auto;

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
      background-color: #a4a4a4;
      border-radius: 16px;
    }

    /* set button(top and bottom of the scrollbar) */
    &::-webkit-scrollbar-button {
        display:none;
    }

    .card {
      width: calc(100% / 5);
      padding: 5px;
      margin: 30px 0;
      position: relative;
      flex-shrink: 0;

      img {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 6px;
      }

      .info-card {
        color: $text-color;
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        opacity: 0;
        padding: 20px 30px;
        border-radius: 6px;
        display: flex;
        flex-direction: column;

        .overview-text {
          font-size: 17px;
          margin: 10px 0;
          line-height: 25px;
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
        }

        .original {
          font-size: 18px;
          margin: 10px 0;
        }

        img {
          width: 30px;
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

        .actors-list {
          margin-top: 10px;
          line-height: 22px;
          font-style: italic;
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