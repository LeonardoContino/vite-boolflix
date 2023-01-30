<script>

export default{
    
    name: 'productionCard',
    data(){
        return{
            placeHolder: '../assets/img/no-poster-available.jpeg'
        }
    },
    props:{
        item: Object
    },
    computed:{
        title(){
            return this.item.title || this.item.name
        },
        originalTitle(){
            return this.item.original_title || this.item.original_name
        },
        hasFlag(){
            const flags = ['it', 'en'];
            return flags.includes(this.item.original_language);
        },
        GetLanguageImg() {
        const url = new URL(`../assets/img/${this.item.original_language}.png`, import.meta.url)
         return url.href;

      
    },
    posterPath(){
        if(!this.item.poster_path) return this.placeHolder;
        return `https://image.tmdb.org/t/p/w342${this.item.poster_path}`
    }
    },
    methods:{
        getVote() {
      return Math.ceil(this.item.vote_average / 2);
      
      
    },
    setStarClass(n){
        let starClass = n <= this.getVote() ? 'fa-solid' : 'fa-regular'
        return starClass + ' fa-star'
    }

    
} }
</script>

<template>

<section>
    <div>
    
    <img :src="posterPath" :alt="item.title">
    
  <ul>
    <li>titolo - {{title }}</li>
    <li>titolo originale - {{ originalTitle }}</li>
    <li>lingua - <img v-if="hasFlag" :src="GetLanguageImg" :alt="item.original_language">
        <div v-else>{{ item.original_language }}</div>
    </li>

    <li>valutazione: <font-awesome-icon  :icon="setStarClass(n)" v-for="n in 5 " /></li>
    <li>trama - {{ item.overview }}</li>

  </ul>
</div>
</section>
</template>


<style scoped lang="scss">

.fa-star{
    color: gold;
    
}


</style>