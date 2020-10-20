<template>
    <div class="bank-availability-wrapper">
        <div class="bank">
            <span>Lo</span>
            <span class="available-mark red"/>
        </div >
        <div class="bank">
            <span>Ro</span>
            <span class="available-mark green"/>
        </div>
    </div>
</template>

<script>
export default {
  props: {
  }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .bank-availability-wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    min-width: 121px;
    border: 1px solid $text-color;
    border-radius: 15px;

    .bank {
        display: flex;
        align-items: center;
        padding: 0 4px;
        
        :nth-child(1) {
            font-weight: 100;
            opacity: 0.2;
            margin-bottom: 3px;
        }

        .available-mark {
            display: inline-block;
            min-height: 24px;
            min-width: 24px;
            margin-left: 4px;
            border-radius: 50%;
    
            &.red {
                background-color: $warning-color;
            }
            &.green {
                background-color: $green-color;
            }
        }
    }

  }

</style>
