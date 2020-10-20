<template>
    <div class="escalator-icon-wrapper">
        <div class="escalator-icon-head">
            <img src="@/assets/icons/roltrap.svg"/>
            <h3>Roltrappen</h3>
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

  .escalator-icon-wrapper {
    display: flex;
    justify-content: space-between;

    .escalator-icon-head {
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
