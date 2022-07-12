<template>
  <div id="app">
    <HeaderComponent @getInputApi="inputApi"/>
    <MainComponent :arrayResult="arrayResult" />
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
      arrayResult: [],
      urlTv: 'https://api.themoviedb.org/3/search/tv?api_key=cd6f03323d12eed84d94ab2ac42d791e&language=it-IT&query=',
      finalTvUrl: '',
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
          this.arrayResult = response.data.results;
        });
        axios.get(this.finalTvUrl)
        .then((response) => {
          this.arrayResult = response.data.results;
          console.log(this.arrayResult)
        })
      } else {
        this.arrayResult = [];
      }
    },
  },
}
</script>

<style lang="scss">
@import url(./assets/scss/style.scss);
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
