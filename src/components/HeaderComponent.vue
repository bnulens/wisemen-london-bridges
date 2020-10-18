<template>
  <header>
    <div v-if="view === 'bridges'" class="bridge-header">
      <div  class="bridge-title-heading">
        <img class="app-logo" src="@/assets/icons/bridge.svg" alt="bridge-logo"/>
        <h1>Bridges</h1>
        <h2>London</h2>
      </div>
      <button @click="onClickNews" class="message-newsfeed"><img class="message-icon" src="@/assets/icons/message.svg" alt="message-newsfeed"></button>
    </div>
    <div v-if="view === 'news'" class="news-header">
      <div  class="title-heading">
        <button @click="onClickBack" class="back-button" >&lt; Vorige</button>
        <h1>Nieuwsberichten</h1>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  props: {
    view: {
      type: String,
      required: true
    }
  },
  methods: {
    onClickNews() {
      console.log('clicked')
      this.$emit('onClickNews')
    },
    onClickBack() {
      console.log('back')
      this.$emit('onClickBack')
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .bridge-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 150px;
    width: 100%;
    padding: 0 16px;
    background-color: $bg-color;
    border-bottom: 1px dotted $warning-color;

    .bridge-title-heading {
      margin-top: 40px;

      .app-logo {
        display: block;
        width: 60px;

        @media screen and (max-width: 767px) {
          display: none;
        }
      }
      
      h1 {
        color: $sec-color;
        font-size: 34px;
        font-weight: 700;
      }

      h2 {
        color: $text-color;
        font-size: 24px;
        font-weight: 400;
      }

      @media screen and (max-width: 767px) {
        
      }
    }

    .message-newsfeed {
      display: block;
      position: relative;
      width: 49px;
      height: 49px;
      margin-top: 40px;
      border-radius: 50%;
      background-color: $info-color;

      .message-icon {
        display: block;
        position: absolute;
        height: 22px;
        width: 27px;
        top: 15px;
        left: 11px;
        // transform: translate(-50%, -50%);
      }
    }
  }

  .news-header {
    height: 150px;
    width: 100%;
    padding: 0 16px;
    background-color: $bg-color;
    border-bottom: 1px dotted $warning-color;
    padding-top: 50px;

    h1 {
      color: $sec-color;
      font-size: 30px;
      font-weight: 700;
    }

    button {
      font-size: 14px;
      color: $text-color;
      background-color: transparent;
      border: none;
      cursor: pointer;
    }
  }
</style>
