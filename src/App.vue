<template>
  <div id="app">
    <HeaderComponent @getInputApi="inputApi"/>
    <MainComponent/>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
import MainComponent from './components/MainComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      searchedText: '',
      finalText: '',
      url: 'https://api.themoviedb.org/3/search/movie?api_key=cd6f03323d12eed84d94ab2ac42d791e&language=it-IT&query=',
      finalUrl: '',
    }
  },
  components: {
    HeaderComponent,
    MainComponent,
  },
  methods: {
    inputApi(searchText) {
      this.searchedText = searchText.toLowerCase();
      this.finalText = this.searchedText.split(' ').join('+');
      this.finalUrl = this.url + this.finalText;
      console.log(this.finalUrl)
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
