<script>

import axios from 'axios';
  
export default{
  data(){
    return{
      searchTerm:'',
      movies: [],
      series:[],
      apiUri: 'https://api.themoviedb.org/3',
      apiKey: '34d4c691860eb29357dea3f73d1e58f2'
    }
    
  },
  methods:{
    GetLanguageImg(img) {
   const url = new URL(`./assets/img/${img}.png`, import.meta.url)
    return url 

      
    },
    searchProductions(query){
      if(!this.searchTerm){
        this.movies = [];
        this.series = [];
        return;
      }
      this.fetchApi('search/movies', 'movies');
      this.fetchApi('search/tv', 'series');

    },
      fetchApi(endpoint,collection){
        const config = {
        params: {
          api_key: this.apiKey,
          query: this.searchTerm  
        }}
    
    axios.get(`${this.apiUri}/${endpoint}`, config)
        .then(res => { this[collection] = res.data.results; })
        .catch(error => { console.log(error) })
      }
      
  
  

    
  
},

}

</script>

<template>
  <header class="container m-3 d-flex justify-content-end">
  <input v-model.trim="searchTerm" type="text">
  <button  @click="searchProductions(searchTerm)">cerca</button>
</header>

<main>
  <section>
  <h3>movies</h3>
  <ul v-for="movie in movies" @key="movie.id">
    <li>titolo - {{ movie.title }}</li>
    <li>titolo originale - {{ movie.original_title }}</li>
    <li>lingua - <img :src="GetLanguageImg(movie.original_language)" :alt="movie.original_language"></li>
    <li>valutazione - {{ movie.vote_average }}</li>
    <li>trama - {{ movie.overview }}</li>

  </ul>
</section>

<section>
  <h3>series</h3>
  <ul v-for="serie in series" @key="serie.id">
    <li>titolo - {{ serie.name }}</li>
    <li>titolo originale - {{ serie.original_name }}</li>
    <li>lingua - <img :src="GetLanguageImg(serie.original_language)" :alt="serie.original_language"></li>
    <li>valutazione - {{ serie.vote_average }}</li>
    <li>trama - {{ serie.overview }}</li>

  </ul>
</section>
</main>
</template>

<style scoped>

</style>
