<script>

import axios from 'axios';
  
export default{
  data(){
    return{
      searchTerm:'',
      movies: [],
      apiUri: 'https://api.themoviedb.org/3',
      apiKey: '34d4c691860eb29357dea3f73d1e58f2'
    }
    
  },
  methods:{
    GetMovies(query){
      const config = {
        params: {
          api_key: this.apiKey,
          query,  
        }
    }
    axios.get(`${this.apiUri}/search/movie`, config)
        .then(res => { this.movies = res.data.results; })
        .catch(error => { console.log(error) })
  },

    
  
},

}

</script>

<template>
  <header class="container m-3 d-flex justify-content-end">
  <input v-model="searchTerm" type="text">
  <button  @click="GetMovies(searchTerm)">cerca</button>
</header>

<main>
  <ul v-for="movie in movies" @key="movies.id">
    <li>titolo - {{ movie.title }}</li>
    <li>titolo originale - {{ movie.original_title }}</li>
    <li>lingua - {{ movie.original_language }}</li>
    <li>valutazione - {{ movie.vote_average }}</li>
    <li>trama - {{ movie.overview }}</li>

  </ul>
</main>
</template>

<style scoped>

</style>
