<template>
  <common-card
    title="累计用户数"
    value="717390"
  >
    <template>
      <div id="totalUserChart" :style="{ width: '100%', height: '100%' }" />
    </template>
    <template v-slot:footer>
      <div class="totalUsersFooter">
        <span>日同比 </span>
        <span class="emphasis">7.90%</span>
        <div class="increase" />
        <span style="margin-left: 10px">月同比 </span>
        <span class="emphasis">3.90%</span>
        <div class="decrease" />
      </div>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from '../mixins/commonCardMixin'
export default {
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById('totalUserChart')
    const chart = this.$echarts.init(chartDom)
    chart.setOption({
      xAxis: {
        type: 'value',
        show: false
      },
      yAxis: {
        type: 'category',
        show: false
      },
      series: [{
        type: 'bar',
        stack: '总量',
        data: [200],
        barWidth: '10px',
        itemStyle: {
          color: '#45c946'
        }
      }, {
        type: 'bar',
        stack: '总量',
        data: [250],
        itemStyle: {
          color: '#eee'
        }
      }, {
        type: 'custom',
        data: [200],
        stack: '总量',
        renderItem: (params, api) => {
          console.log(params, api)
          const value = api.value(0)
          console.log(value)
          const endPoint = api.coord([value, 0])
          console.log(endPoint)

          return {
            type: 'group',
            position: endPoint,
            children: [{
              type: 'path',
              shape: {
                d: 'M535.466667 812.8l450.133333-563.2c14.933333-19.2 2.133333-49.066667-23.466667-49.066667H61.866667c-25.6 0-38.4 29.866667-23.466667 49.066667l450.133333 563.2c12.8 14.933333 34.133333 14.933333 46.933334 0z',
                x: -5,
                y: -15,
                width: 10,
                height: 10,
                layout: 'cover'
              },
              style: {
                fill: '#45c946'
              }
            },
            {
              type: 'path',
              shape: {
                d: 'M512 341.333333l-298.666667 298.666667h597.333334z',
                x: -5,
                y: 3,
                width: 10,
                height: 10,
                layout: 'cover'
              },
              style: {
                fill: '#45c946'
              }
            }
            ]
          }
        }
      }
      ],
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
  .totalUsersFooter {
    display: flex;
    align-items: center;
  }
</style>
