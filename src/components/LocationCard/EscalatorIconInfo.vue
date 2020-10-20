<template>
    <div class="escalator-icon-wrapper">
        <div class="escalator-icon-head">
            <img src="@/assets/icons/roltrap.svg" alt="escalator-image"/>
            <h3>Roltrappen</h3>
        </div>
        <BankAvailability :leftBankInfo="leftBankInfo" :rightBankInfo="rightBankInfo"/>
    </div>
</template>

<script>
import BankAvailability from './BankAvailability'

export default {
  components: {
    BankAvailability
  },
  props: {
    leftBankInfo: {
      type: Object,
      required: true
    },
    rightBankInfo: {
      type: Object,
      required: true
    }
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

        img {
          display: inline-block;
          height: 27;
          width: 25;
        }

        h3 {
          display: inline-block;
          font-size: 16px;
          font-weight: 100;
          margin-left: 12px;
        }
    }
  }
</style>
