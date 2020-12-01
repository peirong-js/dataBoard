<template>
  <div class="topView">
    <el-row :gutter="20">
      <el-col :span="6">
        <el-card shadow="hover">
          <total-sales />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <total-orders />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <today-users />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <total-users />

        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import TotalSales from './TotalSales.vue'
import TodayUsers from './TodayUsers.vue'
import TotalOrders from './TotalOrders.vue'
import TotalUsers from './TotalUsers.vue'
export default {
  name: 'TopView',
  components: {
    TotalSales,
    TodayUsers,
    TotalOrders,
    TotalUsers
  }
}
</script>

<style scoped>
  .topView {
    width: 100%;
  }
</style>
