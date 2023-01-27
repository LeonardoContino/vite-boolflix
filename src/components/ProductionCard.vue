<script>
export default{
    name: 'productionCard',
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

      
    }
    },

    
} 
</script>

<template>

<section>
    <div>
    
        <img :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" :alt="item.title"
                class="img-fluid">
    
  <ul>
    <li>titolo - {{title }}</li>
    <li>titolo originale - {{ originalTitle }}</li>
    <li>lingua - <img v-if="hasFlag" :src="GetLanguageImg" :alt="item.original_language">
        <div v-else>{{ item.original_language }}</div>
    </li>

    <li>valutazione - {{ item.vote_average }}</li>
    <li>trama - {{ item.overview }}</li>

  </ul>
</div>
</section>
</template>