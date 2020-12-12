<template>
  <div class="bottomView">
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="titleWrapper">
            <div class="title">关键词搜索</div>
          </div>
        </template>
        <template>
          <div class="chartWrapper">
            <div class="chartInner">
              <div class="chart">
                <div class="chartTitle">搜索用户数</div>
                <div class="chartData">52463</div>
                <v-chart :options="searchUserOption" />
              </div>
              <div class="chart">
                <div class="chartTitle">搜索量</div>
                <div class="chartData">14545</div>
                <!-- <v-chart :options="searchNumberOption" /> -->
                <v-chart :options="searchUserOption" />
              </div>
            </div>
            <div class="tableWrapper">
              <el-table :data="tableData">
                <el-table-column prop="rank" label="排名" width="180" />
                <el-table-column prop="keyword" label="关键词" width="180" />
                <el-table-column prop="count" label="总搜索量" />
                <el-table-column prop="users" label="搜索用户数" />
              </el-table>
              <el-pagination
                layout="prev, pager, next"
                :total="100"
                :page-size="4"
                background
                @current-change="onPageChange"
              />
            </div>
          </div>

        </template>
      </el-card>
    </div>
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="titleWrapper">
            <div class="title">分类销售排行</div>
            <div class="radioWrapper">
              <el-radio-group v-model="radioSelect" size="small">
                <el-radio-button label="品类" />
                <el-radio-button label="商品" />
              </el-radio-group>
            </div>
          </div>
        </template>
        <template>
          <div class="chartWrapper">
            <v-chart :options="categoryOptions" />
          </div>
        </template>

      </el-card>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BottomView',
  data() {
    return {
      searchUserOption: {
        xAxis: {
          type: 'category',
          boundaryGap: false
        },
        yAxis: {
          show: false
        },
        series: [{
          type: 'line',
          areaStyle: {
            color: 'rgba(95,187,255, 0.5)'
          },
          data: [100, 524, 354, 234, 146, 423],
          lineStyle: {
            color: 'rgb(95,287,255)'
          },
          itemStyle: {
            opacity: 0
          },
          smooth: true
        }],
        grid: {
          top: 0,
          left: 0,
          bottom: 0,
          right: 0
        }
      },
      searchNumberOption: {},
      categoryOptions: {},
      radioSelect: '品类',

      tableData: [
        { id: 1, rank: 1, keyword: '北京', count: 100, users: 90, range: '90%' },
        { id: 2, rank: 1, keyword: '北京', count: 100, users: 90, range: '90%' },
        { id: 3, rank: 1, keyword: '北京', count: 100, users: 90, range: '90%' },
        { id: 4, rank: 1, keyword: '北京', count: 100, users: 90, range: '90%' },
        { id: 5, rank: 1, keyword: '北京', count: 100, users: 90, range: '90%' }
      ]
    }
  },
  mounted() {
    this.renderPieChart()
  },
  methods: {
    onPageChange(page) {
      console.log(page)
    },
    renderPieChart() {
      const mockData = [
        {
          legendname: '粉面粥店',
          value: 67,
          percent: '15.40',
          itemStyle: {
            color: '#8d7fec'
          },
          name: '粉面粥店 | 15.40%'
        },
        {
          legendname: '简餐便当',
          value: 97,
          percent: '22.40',
          itemStyle: {
            color: '#5085f2'
          },
          name: '简餐便当 | 22.40%'
        },
        {
          legendname: '汉堡披萨',
          value: 90,
          percent: '21.80',
          itemStyle: {
            color: '#e7e702'
          },
          name: '汉堡披萨 | 21.80%'
        }
      ]
      this.categoryOptions = {
        title: [{
          text: '品类分布',
          textStyle: {
            fontSize: 14,
            color: '#666'
          },
          left: 20,
          top: 20
        }, {
          text: '累计订单量',
          subtext: '320',
          x: '34.5%',
          y: '42.5%',
          textAlign: 'center',
          textStyle: {
            fontSize: 14,
            color: '#999'
          },
          subtextStyle: {
            fontSize: 28,
            color: '#333'
          }
        }],
        series: [{
          name: '品类分布',
          type: 'pie',
          data: mockData,
          label: {
            normal: {
              show: true,
              position: 'outter',
              formatter: function(params) {
                return params.data.legendname
              }
            }
          },
          center: ['35%', '50%'],
          radius: ['45%', '60%'],
          labelLine: {
            normal: {
              length: 5,
              length2: 3,
              smooth: true
            }
          },
          clockwise: false,
          itemStyle: {
            borderWidth: 4,
            borderColor: '#fff'
          }
        }],
        legend: {
          type: 'scroll',
          orient: 'vertical',
          height: 250,
          left: '70%',
          top: 'middle',
          textStyle: {
            color: '#8c8c8c'
          }
        },
        tooltip: {
          trigger: 'item',
          formatter: function(params) {
            const str = params.seriesName + '<br />' +
                        params.marker + params.data.legendname + '<br />' +
                        '数量：' + params.data.value + '<br />' +
                        '占比：' + params.data.percent + '%'
            return str
          }
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .bottomView {
    display: flex;
    margin-top: 20px;
    .view {
      flex: 1;
      width: 50%;
      box-sizing: border-box;
      &:first-child {
        padding: 0 10px 0 0;
      }
      &:last-child {
        padding: 0 0 0 10px;
      }
      .titleWrapper {
        display: flex;
        align-items: center;
        height: 60px;
        box-sizing: border-box;
        border-bottom: 1px solid #eee;
        font-size: 14px;
        font-weight: 500;
        padding: 0 0 0 20px;
        .radioWrapper {
          flex: 1;
          display: flex;
          justify-content: flex-end;
          padding-right: 20px;
        }
      }
      .chartWrapper{
        display: flex;
        flex-direction: column;
        height: 452px;
        .chartInner {
          display: flex;
          padding: 0 10px;
          margin-top: 20px;
          .chart {
            flex: 1;
            padding: 0 10px;
            .chartTitle {
              color: #999;
              font-size: 14px;
            }
            .chartData {
              font-size: 22px;
              color: #333;
              font-weight: 500;
              letter-spacing: 2px;
            }
            .echarts {
              height: 50px;
            }
          }
        }
        .tableWrapper {
          flex: 1;
          margin-top: 20px;
          padding: 0 20px 20px;
          .el-pagination {
            display: flex;
            justify-content: flex-end;
            margin-top: 15px;
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
