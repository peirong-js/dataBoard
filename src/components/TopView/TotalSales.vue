<template>
  <common-card
    title="累计销售额"
    value="￥ 200"
  >
    <template>
      <div class="compareWrapper">
        <div class="compare">
          <span>日同比 </span>
          <span class="emphasis">7.90%</span>
          <div class="increase" />
        </div>
        <div class="compare">
          <span>月同比 </span>
          <span class="emphasis">9.90%</span>
          <div class="decrease" />

        </div>
      </div>
    </template>
    <template v-slot:footer>
      <span>昨日销售额 </span>
      <span class="emphasis">￥ 30000</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from '../mixins/commonCardMixin'
export default {
  mixins: [commonCardMixin]

}
</script>

<style lang="scss" scoped>
  .compareWrapper {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    .compare {
        font-size: 12px;
        margin-top: 3px;
        color: #666;
        display: flex;
        align-items: center;
      }
  }

</style>
