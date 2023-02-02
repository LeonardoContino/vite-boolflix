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


    <div class="card mb-4">
    
        <div class="col">
            <div class="copertina">
                <img class="img-fluid" :src="posterPath" :alt="item.title">
            </div>  
            <div class="p-description">
                <h3>titolo - {{title }}</h3>
                <h4>titolo originale - {{ originalTitle }}</h4>
                <div>lingua - <img class="img-lang" v-if="hasFlag" :src="GetLanguageImg" :alt="item.original_language">
                    <div v-else>{{ item.original_language }}</div>
                </div>

                <div>valutazione: <font-awesome-icon  :icon="setStarClass(n)" v-for="n in 5 "></font-awesome-icon></div>
                <p>trama - {{ item.overview }}</p>
            </div>

        </div>
    </div>

</template>


<style scoped lang="scss">
.card{
    height: 500px;
    position: relative;
    width: 350px;
    background-color: black;
    cursor: pointer;
    
    .col{
        height: 500px;
        width: 100%;
        
    }
}
.copertina{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    
    img{
        width: 100%;
        height: 100%;
        
    }
    

}
.copertina:hover{
    display: none;
    transition: 0.5s;
    
    
}
.p-description {
    padding-top: 20px;
   overflow-y: auto;
   color: white;
   height: 100%;
   width: 100%;
   
}

.img-lang{
    width: 40px;
}
.fa-star{
    color: gold;
    
}


</style>