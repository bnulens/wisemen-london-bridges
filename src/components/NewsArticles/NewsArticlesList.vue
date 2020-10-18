<template>
    <ul>
        <!-- <li v-for="article in articles" :key="article.id">{{ article.title }}</li>    -->
        <NewsArticleSmall v-for="article in articles" :key="article.id" v-bind:article="article"/>
    </ul>
</template>

<script>
import axios from 'axios'
import NewsArticleSmall from './NewsArticleSmall'
// import NewsArticleDetail from './NewsArticleDetail'

export default {
    components: {
        NewsArticleSmall,
        // NewsArticleDetail
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

  ul {
      height: 100%;
      overflow: scroll;
  }
</style>
