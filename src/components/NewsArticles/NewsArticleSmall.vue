<template>
  <li class="news-article-list-item">
    <article class="news-article-small">
      <img :src="`https://awv-fietsverbindingen.development.appwi.se${article.image_url}`" alt="article-image"/>
      <div class="news-article-small-info">
        <h3>{{ article.title }}</h3>
        <time :datetime="getDate(article.created_at)">{{ getDate(article.created_at) }}</time>
        <div class="news-article-small-info-description">
          <p>{{article.description}}</p>
        </div>
      </div>
      <button @click="toggleDetail()" class="toggle-detail">&gt;</button>
    </article>
  </li>
</template>

<script>

export default {
  props: {
    article: { type: Object, required: true }
  },
  methods: {
    getDate(str) {
      const newDate = new Date(str);
      const readDate = newDate.toLocaleDateString("en-GB", {weekday: 'short',day: '2-digit', month: '2-digit', year: '2-digit', hour: '2-digit', minute:'2-digit'});
      return readDate;
    },
    toggleDetail() {
      console.log('Toggled')
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .news-article-list-item {
    display: block;
    position: relative;
    padding-left: 15px;
    background-color: $bg-color;

    @media screen and (max-width: 768px) {

      &:before {
        content: "";
        display: block;
        position: absolute;
        top: 3px;
        left: 0;
        height: 96%;
        width: 4px;
        background-color: $sec-color;
        border-radius: 25px;
      }
    }

    .news-article-small {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 0;
      border-bottom: 1px solid $text-color;

      img {
        display: block;
        height: 117px;
        width: 87px;
        margin-right: 4px;
        border-radius: 3px;
      }

      .news-article-small-info {
        width: 70%;
        padding-right: 15px;
        font-weight: 100;
        text-align: justify;

        h3 {
          color: $sec-color;
          font-size: 18px;
          font-weight: 400;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }

        time {
          display: block;
          color: $text-color;
          font-size: 12px;
          text-transform: uppercase;
        }

        .news-article-small-info-description {
          display: -webkit-box;
          margin-top: 12px;
          -webkit-line-clamp: 4;
          -webkit-box-orient: vertical; 
          overflow: hidden;
          text-overflow: ellipsis;

          p {
            font-size: 15px;
            color: $text-color;
            line-height: 1.2;
          }
        }
      }

      button.toggle-detail {
        margin: 0 8px;
        color: $sec-color;
        font-size: 20px;
        background-color: transparent;
        border: none;
      }
    }
  }
</style>
