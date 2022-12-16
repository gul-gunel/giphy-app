<template>
  <div id="app">
    <Search @search-requested="handleSearch" />
    <p v-if="isLoading">Loading</p>
    <Preview :gifs="gifs" />
  </div>
</template>

<script>
import Search from './components/SearchCom.vue';
import Preview from './components/PreviewCom.vue';

export default {
  name: "App",
  components: { Search, Preview },
  data() {
    return {
      isLoading: false,
      gifs: [],
      API_KEY: `TIWhWBzGnNWfgfWcU3fFu5uCJILzGB7H`,
    }
  },
  methods: {
    doQuery(url){
      fetch(url)
        .then(res => res.json())
        .then(res => {
          this.gifs = res.data;
          this.isLoading = false;
        })
        .catch(err => console.error(err))
    },
    handleSearch(query) {
      this.gifs = [];
      this.isLoading = true;
      // sorular
      // 1- URL' ler data alanında mı olmalı?  *** trim()
      const URL = `https://api.giphy.com/v1/gifs/trending?api_key=${this.API_KEY}`
      const URL_S = `https://api.giphy.com/v1/gifs/search?api_key=${this.API_KEY}&q=${query}`;      
      if(query.trim() != ""){
        this.doQuery(URL_S)
      }else{
        this.doQuery(URL)
      }
    }
  },
  created() {
    const URL = `https://api.giphy.com/v1/gifs/trending?api_key=${this.API_KEY}`
    this.doQuery(URL);      
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
