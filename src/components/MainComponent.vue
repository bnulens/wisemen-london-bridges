<template>
  <main>
    <NewsArticleList :class="isBridgeView ? 'show-news' : 'hide-news'"/>
    <MapBoxMap/>
  </main>
</template>

<script>
import NewsArticleList from './NewsArticles/NewsArticlesList'
import MapBoxMap from './BridgeMap/MapBoxMap'

export default {
  components: {
    NewsArticleList,
    MapBoxMap,
  }, 
  props: {
    view: {
      type: String,
      required: true
    }
  },
  computed: {
    isBridgeView() {
      if (this.view === 'bridges') {
        return true
      }
      return false
    }
  }
}
</script>

<style lang="scss" scoped>
  .show-news {
    transition: all ease-in 0.6s;

    @media screen and (max-width: 768px) {
      display: none;
      transition: all ease-in 0.6s;
    }
  }
</style>
