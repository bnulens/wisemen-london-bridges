<template>
    <div class="lift-icon-wrapper">
        <div class="lift-icon-head">
            <img src="@/assets/icons/lift.svg"/>
            <h3>Liften</h3>
        </div>
        <BankAvailability/>
    </div>
</template>

<script>
import BankAvailability from './BankAvailability'
export default {
    components: {
        BankAvailability
    },
    props: {
    }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .lift-icon-wrapper {
    display: flex;
    justify-content: space-between;
    margin-bottom: 6px;

    .lift-icon-head {
        display: flex;
        align-items: center;
        h3 {
            display: inline-block;
            font-size: 20px;
            font-weight: 100;
            margin-left: 6px;
        }
    }
  }
</style>
