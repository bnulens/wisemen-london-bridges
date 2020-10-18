<template>
  <li class="news-article-list-item">
    <article class="news-article-small">
      <img :src="`https://awv-fietsverbindingen.development.appwi.se${article.image_url}`" alt="x"/>
      <div class="news-article-small-info">
        <h3>{{ article.title }}</h3>
        <time :datetime="getDate(article.created_at)">{{ getDate(article.created_at) }}</time>
        <div class="news-article-small-info-description">
          <p>{{article.description}}</p>
        </div>
      </div>
    </article>
  </li>
</template>

<script>
export default {
  props: {
    article: { type: Object, required: true }
  },
  methods: {
    getDate: (str) => {
      const newDate = new Date(str);
      const readDate = newDate.toLocaleDateString("en-GB", {weekday: 'short',day: '2-digit', month: '2-digit', year: '2-digit', hour: '2-digit', minute:'2-digit'});
      return readDate;
    }
  }
}

</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .news-article-list-item {
    display: block;
    position: relative;
    height: 149px;
    width: 100%;
    padding-left: 15px;
    overflow: hidden;

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

    .news-article-small {
      display: flex;
      align-items: center;
      height: 100%;
      padding-top: 10px;
      padding-bottom: 10px;
      border-bottom: 1px solid $text-color;

      img {
        display: block;
        height: 117px;
        width: 87px;
        margin-right: 13px;
        border-radius: 3px;
      }

      .news-article-small-info {
        width: 70%;
        height: 100%;
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
          -webkit-line-clamp: 3;
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
    }
  }
</style>
