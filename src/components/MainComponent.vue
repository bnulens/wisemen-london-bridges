<template>
  <main>
    <NewsArticleList :class="isBridgeView ? 'show-news' : 'hide-news'"/>
    <MapBoxMap/>
    <!-- <Map/> -->
  </main>
</template>

<script>
import NewsArticleList from './NewsArticles/NewsArticlesList'
import MapBoxMap from './BridgeMap/MapBoxMap'
// import Map from './BridgeMap/Map'

export default {
  components: {
    NewsArticleList,
    MapBoxMap,
    // Map
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
    @media screen and (max-width: 768px) {
      display: none;
    }
  }
</style>
