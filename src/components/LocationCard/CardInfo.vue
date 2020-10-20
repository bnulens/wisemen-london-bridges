<template>
    <div class="card-info-wrapper">
        <span>
            <img :src="getIcon()" alt="info-icon"/>
        </span>
        <div>
            <h4>{{ title }}</h4>
            <p>{{ content }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        icon: {
            type: String,
            required: true
        },
        title: {
            type: String,
            required: true
        },
        content: {
            type: String,
            required: true
        }
    },
    methods: {
        getIcon() {
            return require(`../../assets/icons/${this.icon}.svg`);
        }
    }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .card-info-wrapper {
    display: flex;
    justify-content: space-between;
    margin: 24px 0;

    img {
        margin-right: 12px;
    }

    p {
        font-size: 12px;
        font-weight: 100;
    }
    
  }
</style>
