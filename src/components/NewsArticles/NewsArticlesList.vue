<template>
   <div>
        <ul class="news-article-list">
            <NewsArticleSmall v-for="article in articles" :key="article.id" :article="article"/>
        </ul>
   </div>
</template>

<script>
import axios from 'axios'
import NewsArticleSmall from './NewsArticleSmall'

export default {
    components: {
        NewsArticleSmall,
    },
    data() {
        return {
            articles: [],
        }
    },
    mounted() {
        axios
            .get('https://awv-fietsverbindingen.development.appwi.se/api/news')
            .then( res => (this.articles = res.data))
    },

}
</script>
<style lang="scss" scoped>
    .news-article-list {
        position: absolute;
        z-index: 550;
        transition: all ease-in 0.6s;
        
        @media screen and (min-width: 768px) {
            height: 100vh;
            max-width: 25%;
            overflow: scroll;
            transition: all ease-in 0.6s;
        }
    }
</style>
