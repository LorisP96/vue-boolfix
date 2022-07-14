<template>
  <div id="app">
    <HeaderComponent @getInputApi="inputApi"/>
    <MainComponent :arrayFilmResult="arrayFilmResult" :arrayTvResult="arrayTvResult" />
  </div>
</template>

<script>
import axios from 'axios';
import HeaderComponent from './components/HeaderComponent.vue';
import MainComponent from './components/MainComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      searchText: '',
      finalText: '',
      urlFilm: 'https://api.themoviedb.org/3/search/movie?api_key=cd6f03323d12eed84d94ab2ac42d791e&language=it-IT&query=',
      finalFilmUrl: '',
      arrayFilmResult: [],
      urlTv: 'https://api.themoviedb.org/3/search/tv?api_key=cd6f03323d12eed84d94ab2ac42d791e&language=it-IT&query=',
      finalTvUrl: '',
      arrayTvResult: [],
    }
  },
  components: {
    HeaderComponent,
    MainComponent,
  },
  methods: {
    inputApi(searchText) {
      this.finalText = searchText.split(' ').join('+');
      this.finalFilmUrl = this.urlFilm + this.finalText;
      this.finalTvUrl = this.urlTv + this.finalText;
      if(this.finalText !== '') {
        axios.get(this.finalFilmUrl)
        .then((response) => {
          this.arrayFilmResult = response.data.results;
        });
        axios.get(this.finalTvUrl)
        .then((response) => {
          this.arrayTvResult = response.data.results;
        })
      } else {
        this.arrayFilmResult = [];
        this.arrayTvResult = [];
      }
    },
  },
}
</script>

<style lang="scss">
@import './assets/scss/style.scss';
@import './assets/scss/variables.scss';
@import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@300;400;700&family=Montserrat:wght@300;400;700&family=Nunito+Sans:wght@300;600&family=Open+Sans:wght@500;700&family=PT+Sans:wght@400;700&family=Raleway&family=Rock+Salt&family=WindSong:wght@400;500&display=swap');
#app {
  font-family: 'Nunito Sans', sans-serif;
}
</style>
