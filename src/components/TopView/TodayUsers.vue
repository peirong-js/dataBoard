<template>
  <common-card
    title="今日交易用户"
    value="604920"
  >
    <template>
      <div id="todayUserChart" :style="{ width: '100%', height: '100%' }" />
    </template>
    <template v-slot:footer>
      <span>退款率 </span>
      <span class="emphasis">7.17%</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from '../mixins/commonCardMixin'
export default {
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById('todayUserChart')
    const chart = this.$echarts.init(chartDom)
    chart.setOption({
      xAxis: {
        type: 'category',
        show: false,
        data: ['00:00', '01:00', '02:00', '03:00', '04:00', '05:00', '06:00']
      },
      yAxis: {
        show: false
      },
      series: [{
        type: 'bar',
        data: [30, 20, 60, 56, 20, 57, 29],
        barWidth: '60%'
      }],
      color: ['#3398db'],
      tooltip: {},
      grid: {
        top: 0,
        left: 0,
        right: 0,
        bottom: 0
      }
    })
  }

}
</script>

<style lang="scss" scoped>

</style>
