<template>
  <div class="content-wrapper">
    <div class="dashboard-container">
      <div class="dashboard-row">
        <div class="dashboard-left">
          <div class="card">
            <h3 class="card-title">系统状态</h3>
            <div class="chart-container">
              <canvas ref="systemChartRef"></canvas>
            </div>
          </div>
        </div>
        <div class="dashboard-right">
          <div class="card">
            <h3 class="card-title">任务组</h3>
            <div class="chart-container">
              <canvas ref="taskChartRef"></canvas>
            </div>
          </div>
        </div>
      </div>
      <div class="dashboard-row">
        <div class="dashboard-left" style="flex: 7;">
          <div class="card">
            <h3 class="card-title">任务进度</h3>
            <table class="data-table">
              <thead>
                <tr>
                  <th>任务ID</th>
                  <th>任务名称</th>
                  <th>进度</th>
                  <th>状态</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>001</td>
                  <td>IP数据库更新</td>
                  <td>
                    <div class="progress-bar"><div class="progress-fill" style="width: 75%;"></div></div>
                    <span>75%</span>
                  </td>
                  <td><span class="status running">运行中</span></td>
                </tr>
                <tr>
                  <td>002</td>
                  <td>端口扫描</td>
                  <td>
                    <div class="progress-bar"><div class="progress-fill" style="width: 30%;"></div></div>
                    <span>30%</span>
                  </td>
                  <td><span class="status running">运行中</span></td>
                </tr>
                <tr>
                  <td>003</td>
                  <td>威胁检测</td>
                  <td>
                    <div class="progress-bar"><div class="progress-fill" style="width: 100%;"></div></div>
                    <span>100%</span>
                  </td>
                  <td><span class="status completed">已完成</span></td>
                </tr>
                <tr>
                  <td>004</td>
                  <td>日志分析</td>
                  <td>
                    <div class="progress-bar"><div class="progress-fill" style="width: 0%;"></div></div>
                    <span>0%</span>
                  </td>
                  <td><span class="status pending">等待中</span></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        <div class="dashboard-right" style="flex: 3;">
          <div class="card">
            <h3 class="card-title">系统信息</h3>
            <table class="info-table">
              <tbody>
              <tr><td>服务器</td><td>Linux localhost</td></tr>
              <tr><td>CPU使用</td><td>45%</td></tr>
              <tr><td>内存使用</td><td>62%</td></tr>
              <tr><td>磁盘使用</td><td>38%</td></tr>
              <tr><td>在线用户</td><td>3</td></tr>
              <tr><td>运行时间</td><td>42天 7小时</td></tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.dashboard-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.dashboard-row {
  display: flex;
  gap: 20px;
}
.dashboard-left {
  flex: 1;
}
.dashboard-right {
  flex: 1;
}
.card {
  background: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}
.card-title {
  margin: 0 0 16px 0;
  font-size: 16px;
  font-weight: 600;
  color: #333;
}
.chart-container {
  width: 100%;
  height: 200px;
  display: flex;
  justify-content: center;
}
.info-table {
  width: 100%;
  border-collapse: collapse;
}
.info-table td {
  padding: 10px 12px;
  border-bottom: 1px solid #f0f0f0;
  color: #333;
  font-size: 14px;
}
.info-table td:first-child {
  color: #666;
  width: 100px;
}
.info-table tr:last-child td {
  border-bottom: none;
}
.progress-bar {
  width: 60%;
  height: 8px;
  background: #f0f0f0;
  border-radius: 4px;
  display: inline-block;
  vertical-align: middle;
  margin-right: 8px;
}
.progress-fill {
  height: 100%;
  background: #1890ff;
  border-radius: 4px;
}
.status {
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 12px;
}
.status.running { background: #e6f7ff; color: #1890ff; }
.status.completed { background: #f6ffed; color: #52c41a; }
.status.pending { background: #f5f5f5; color: #999; }
</style>

<script setup>
import { ref, onMounted } from 'vue'
import { Chart, ArcElement, DoughnutController, PieController, Legend, Tooltip } from 'chart.js'
Chart.register(ArcElement, DoughnutController, PieController, Legend, Tooltip)

const systemChartRef = ref(null)
const taskChartRef = ref(null)

onMounted(() => {
  const ctx = systemChartRef.value.getContext('2d')
  new Chart(ctx, {
    type: 'doughnut',
    data: {
      labels: ['CPU', '内存', '磁盘', '其他'],
      datasets: [{
        data: [45, 62, 38, 20],
        backgroundColor: ['#1890ff', '#52c41a', '#faad14', '#f0f0f0'],
        borderWidth: 0
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      cutout: '65%',
      plugins: {
        legend: {
          position: 'bottom',
          labels: {
            padding: 15,
            usePointStyle: true,
            font: { size: 12 }
          }
        }
      }
    }
  })

  const taskCtx = taskChartRef.value.getContext('2d')
  new Chart(taskCtx, {
    type: 'pie',
    data: {
      labels: ['AI智能体', '管理员'],
      datasets: [{
        data: [3, 1],
        backgroundColor: ['#1890ff', '#52c41a'],
        borderWidth: 0
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: {
          position: 'bottom',
          labels: {
            padding: 15,
            usePointStyle: true,
            font: { size: 12 }
          }
        }
      }
    }
  })
})
</script>