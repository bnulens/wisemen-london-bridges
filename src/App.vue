<template>
  <div>
    <HeaderComponent :view="view" @news="view = 'news'" @back="view = 'bridges'"/>
    <MainComponent :view="view" /> 
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent'
import MainComponent from './components/MainComponent'

export default {
  components: {
    HeaderComponent,
    MainComponent
  },
  data() {
    return {
      view: "bridges"
    }
  }
}
</script>

<style lang="scss">
  @import './assets/scss/global.scss';
</style>
