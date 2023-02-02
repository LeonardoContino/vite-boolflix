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
  <header class="container d-flex justify-content-between align-items-center">
  <h1 class="text-danger">BOOLFLIX</h1>
  <div class="d-flex">
    <input v-model.trim="searchTerm" type="text" class="form-control input-header">
  <button class="btn btn-danger ms-2" @click="searchProductions(searchTerm)">cerca</button>
  </div>
  
</header>

<main class="container">
  <section >
  <h3>movies</h3>
  <div class="row row-cols-4 m-0 gap-5 justify-content-center">
  <ProductionCard v-for="movie in this.movies" :key="movie.id" :item="movie"></ProductionCard>

  </div>
</section>

<section >
  <h3>series</h3>
  <div class="row row-cols-4 g-3 m-0 gap-5 justify-content-center ">
  <ProductionCard v-for="serie in this.series" :key="serie.id" :item="serie"></ProductionCard>

  </div>
  
</section>
</main>
</template>

<style scoped lang="scss">
header{
  background-color: black;
  padding-top: 20px;
  padding-bottom: 20px;
  
  .input-header{
    width: 300px;
    height: 40px;
    padding: 0px;
    padding-right: 10px;
  }
  button{
    height: 40px;
  }

}
main{
  background-color: #555555;
  min-height: calc(100vh - 80px);

  h3{
  padding-top: 10px;
  color: white;
}
}

</style>
