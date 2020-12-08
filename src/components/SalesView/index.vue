<template>
  <div class="salesView">
    <el-card shadow="hover">
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
        <div>22</div>
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
      }
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
  }

  ::v-deep .el-card__header {
    border-bottom: none;
    padding: 0;
  }
</style>
