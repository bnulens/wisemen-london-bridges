<template>
   <div class="news-article-list-wrapper">
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
        NewsArticleSmall
    },
    data() {
        return {
            articles: []
        }
    },
    mounted() {
        axios
            .get('https://awv-fietsverbindingen.development.appwi.se/api/news')
            .then( res => (this.articles = res.data))
    }
}
</script>
<style lang="scss" scoped>
    @import '@/assets/scss/_vars.scss';
    .news-article-list-wrapper {
        z-index: 550;
        background-color: $bg-color;

        .news-article-list {
            position: relative;
            transition: all ease-in 0.6s;
            
            @media screen and (min-width: 768px) {
                position: relative;
                width: 100%;
                overflow: scroll;
                transition: all ease-in 0.6s;
            }
        }
        @media screen and (min-width: 768px) {
            display: block;
            width: 30%;
            background-color: $bg-color;
            overflow: scroll;
        }
    }
</style>
