<template>
  <common-card
    title="累计订单量"
    value="200"
  >
    <template>
      <div id="totalOrderChart" :style="{ width: '100%', height: '100%' }" />
    </template>
    <template v-slot:footer>
      <span>昨日昨日订单量 </span>
      <span class="emphasis">￥ 30000</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from '../mixins/commonCardMixin'
export default {
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById('totalOrderChart')
    const chart = this.$echarts.init(chartDom, 'light', { renderer: 'svg' })
    chart.setOption({
      xAxis: {
        type: 'category',
        show: false,
        boundaryGap: false
      },
      yAxis: {
        show: false
      },
      series: [{
        type: 'line',
        data: [20, 34, 5, 39, 18, 30, 28, 49, 18],
        areaStyle: {
          color: 'green'
        },
        lineStyle: {
          width: 0
        },
        itemStyle: {
          opacity: 0
        },
        smooth: true
      }],
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

<style scoped>

</style>
