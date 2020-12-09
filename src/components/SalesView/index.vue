<template>
  <div class="salesView">
    <el-card shadow="hover" :body-style="{ padding: '0 0 20px 0' }">
      <template v-slot:header>
        <div class="menuWrapper">
          <el-menu
            :default-active="activeIndex"
            mode="horizontal"
            class="salesViewMenu"
            @select="onMenuSelect"
          >
            <el-menu-item index="1">销售额</el-menu-item>
            <el-menu-item index="2">访问量</el-menu-item>
          </el-menu>
          <div class="menuRight">
            <el-radio-group v-model="radioSelect" size="small">
              <el-radio-button label="今日" />
              <el-radio-button label="本周" />
              <el-radio-button label="本月" />
              <el-radio-button label="今年" />
            </el-radio-group>
            <el-date-picker
              v-model="date"
              type="daterange"
              range-separator="至"
              start-placeholde="开始日期"
              end-placeholde="结束日期"
              size="small"
              unlink-panels
              :picker-options="pickerOptions"
              class="datePick"
            />
          </div>
        </div>
      </template>
      <template>
        <div class="salesViewChartWrapper">
          <v-chart :options="chartOption" />
          <div class="salesViewList">
            <div class="salesViewTitle">排行榜</div>
            <div class="listItemWrapper">
              <div v-for="item in rankData" :key="item.no" class="listItem">
                <div :class="['listItemNo', +item.no <=3 ? 'topNo' : '']">{{ item.no }}</div>
                <div class="listItemName">{{ item.name }}</div>
                <div class="listItemMoney">{{ item.money }}</div>
              </div>
            </div>

          </div>
        </div>
      </template>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'SalesView',
  data() {
    return {
      activeIndex: '1',
      radioSelect: '今日',
      date: null,
      pickerOptions: {
        shortcuts: [{
          text: '最近一周',
          onClick(picker) {
            const start = new Date()
            const end = new Date()
            start.setTime(start.getTime() - 3600 * 24 * 1000 * 7)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近一个月',
          onClick(picker) {
            const start = new Date()
            const end = new Date()
            start.setTime(start.getTime() - 3600 * 24 * 1000 * 30)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近三个月',
          onClick(picker) {
            const start = new Date()
            const end = new Date()
            start.setTime(start.getTime() - 3600 * 24 * 1000 * 90)
            picker.$emit('pick', [start, end])
          }
        }]
      },
      chartOption: {
        title: {
          text: '年度销售额',
          textStyle: {
            fontSize: 12,
            color: '#666'
          },
          left: 20,
          top: 20
        },
        xAxis: {
          type: 'category',
          data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
          axisTick: {
            alignWithLabel: true,
            lineStyle: {
              color: '#999'
            }
          },
          axisLine: {
            lineStyle: {
              color: '#999'
            }
          },
          axisLabel: {
            color: '#333'
          }
        },
        yAxis: {
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          splitLine: {
            lineStyle: {
              type: '#dotted',
              color: '#eee'
            }
          }
        },
        series: [{
          type: 'bar',
          barWidth: '35%',
          data: [200, 250, 300, 500, 200, 250, 300, 500, 200, 250, 300, 500]
        }],
        grid: {
          top: 70,
          left: 60,
          right: 60,
          bottom: 50
        },
        color: ['#3398db']
      },
      rankData: [{
        no: 1,
        name: '麦当劳',
        money: '32398'
      }, {
        no: 2,
        name: '麦当劳',
        money: '32398'
      }, {
        no: 3,
        name: '麦当劳',
        money: '32398'
      }, {
        no: 4,
        name: '麦当劳',
        money: '32398'
      }, {
        no: 5,
        name: '麦当劳',
        money: '32398'
      }, {
        no: 6,
        name: '麦当劳',
        money: '32398'
      }, {
        no: 7,
        name: '麦当劳',
        money: '32398'
      }]
    }
  },
  methods: {
    onMenuSelect(index) {
      this.activeIndex = index
    }
  }
}
</script>

<style lang="scss" scoped>
  .salesView {
    margin-top: 20px;
    .menuWrapper {
      position: relative;
      display: flex;
      .salesViewMenu {
        width: 100%;
        padding-left: 20px;
        .el-menu-item {
          height: 50px;
          line-height: 50px;
          margin: 0 20px;
        }
      }
      .menuRight {
        position: absolute;
        right: 20px;
        top: 0;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: flex-end;
        .datePick {
          margin-left: 20px;
        }
      }
    }
    .salesViewChartWrapper {
      display: flex;
      height: 270px;
      .echarts {
        flex: 0 0 70%;
        width: 70%;
        height: 100%;
      }
      .salesViewList {
        flex: 1;
        width: 100%;
        height: 100%;
        overflow: hidden;
          margin-top: 15px;
        .salesViewTitle{
          margin-top: 20px;
          font-size: 12px;
          color: #666;
          font-weight: 500;
        }
        .listItemWrapper {
          margin-top: 15px;
          .listItem {
            display: flex;
            align-items: center;
            font-size: 12px;
            height: 20px;
            padding: 6px 20px 6px 0;
            .listItemNo {
              display: flex;
              align-items: center;
              justify-content: center;
              width: 20px;
              height: 20px;
              color: #333;
              &.topNo {
                background: #000;
                border-radius: 50%;
                font-weight: 500;
              }
            }
            .listItemName {
              margin-left: 10px;
              color: #333;
            }
            .listItemMoney {
              flex: 1;
              text-align: right;
            }
          }
        }

      }
    }
  }

  ::v-deep .el-card__header {
    border-bottom: none;
    padding: 0;
  }
</style>
