<script>

import axios from 'axios';
import ProductionCard from './components/ProductionCard.vue';
  
export default{
  components:{ProductionCard},
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
    searchProductions(query){
      if(!this.searchTerm){
        this.movies = [];
        this.series = [];
        return;
      }
      this.fetchApi('search/movie', 'movies');
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
  <ProductionCard v-for="movie in this.movies" :key="movie.id" :item="movie"></ProductionCard>
</section>

<section>
  <h3>series</h3>
  <ProductionCard v-for="serie in this.series" :key="serie.id" :item="serie"></ProductionCard>
  
</section>
</main>
</template>

<style scoped>

</style>
