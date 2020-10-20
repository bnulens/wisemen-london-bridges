<template>
  <header>
    <div v-if="view === 'bridges'" class="bridge-header">
      <div  class="bridge-title">
        <img src="@/assets/icons/bridge.svg" alt="bridge-logo"/>
        <div class="bridge-title-heading">
          <h1>Bridges</h1>
          <h2>London</h2>
        </div>
      </div>
      <button @click="onClickNews" class="message-newsfeed"><img class="message-icon" src="@/assets/icons/message.svg" alt="message-newsfeed"></button>
    </div>
    <div v-if="view === 'news'" class="news-header">
      <div  class="title-heading">
        <button @click="onClickBack" class="back-button" >&lsaquo; Vorige</button>
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
      this.$emit('news')
    },
    onClickBack() {
      this.$emit('back')
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .bridge-header {
    position: absolute;
    display: flex;
    justify-content: space-between;
    align-items: center;
    top: 0;
    height: 150px;
    width: 100%;
    padding: 0 16px;
    background-color: $bg-color;
    z-index: 1001;

    .bridge-title {
      margin-top: 40px;

      img {
        display: block;
        width: 45%;
        max-width: 300px;
        
        @media screen and (max-width: 768px) {
          display: none;
        }
      }
      
      .bridge-title-heading {
        display: flex;
        flex-direction: column;

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
      }

      @media screen and (min-width: 768px) {
        display: flex;
        align-items: center;
        margin-top: 0;
        line-height: 1.2;
        
        img {
          margin-right: 12px;
        }
        .bridge-title-heading {

          h1 {
            font-size: 18px;
          }
  
          h2 {
            font-size: 14px;
          }
        }
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
      }
    }
    @media screen and (min-width: 768px) {
      position: relative;
      align-items: center;
      height: 105px;

      .message-newsfeed {
        display: none;
      }
    }
  }

  .news-header {
    position: absolute;
    top: 0;
    height: 150px;
    width: 100%;
    padding: 0 16px;
    background-color: $bg-color;
    padding-top: 50px;
    z-index: 1001;

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
