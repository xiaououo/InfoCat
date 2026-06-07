<template>
  <div class="content-wrapper">
    <div class="tab-bar">
      <div class="tab" :class="{ active: activeTab === 'tab1' }" @click="activeTab = 'tab1'">HFish-运行状态</div>
      <div class="tab" :class="{ active: activeTab === 'tab2' }" @click="activeTab = 'tab2'">攻击者列表</div>
    </div>
    <div class="tab-content-wrapper">
      <div class="tab-content" :class="{ active: activeTab === 'tab1' }">
        <table class="data-table">
          <thead><tr><th>节点名称</th><th>节点IP</th><th>时间戳</th></tr></thead>
          <tbody>
            <tr v-for="(item, idx) in hfishData" :key="idx">
              <td>{{ item.name }}</td>
              <td>{{ item.ip }}</td>
              <td>{{ item.create_time }}</td>
            </tr>
          </tbody>
        </table>
        <div class="pagination">
          <span class="pagination-info">共 {{ hfishData.length }} 条</span>
          <div class="pagination-right"><div class="pagination-buttons"><button class="page-btn" disabled>上一页</button><button class="page-btn active">1</button><button class="page-btn" disabled>下一页</button></div></div>
        </div>
      </div>

      <div class="tab-content" :class="{ active: activeTab === 'tab2' }">
        <table class="data-table">
          <thead>
            <tr>
              <th class="col-id">ID</th>
              <th class="text">IP地址</th>
              <th class="text">地理位置</th>
              <th class="col-date">首次发现</th>
              <th class="col-date">最近攻击</th>
              <th class="col-num">攻击次数</th>
              <th class="col-action">操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, idx) in attackerData" :key="idx">
              <td class="col-id">{{ item.id }}</td>
              <td class="text">{{ item.ip }}</td>
              <td class="text">{{ item.location }}</td>
              <td class="col-date">{{ item.first }}</td>
              <td class="col-date">{{ item.last }}</td>
              <td class="col-num">{{ item.count }}</td>
              <td class="col-action"><button class="btn btn-primary btn-sm">添加至任务</button></td>
            </tr>
          </tbody>
        </table>
        <div class="pagination">
          <span class="pagination-info">共 {{ attackerData.length }} 条</span>
          <div class="pagination-buttons">
            <button class="page-btn" disabled>上一页</button>
            <button class="page-btn active">1</button>
            <button class="page-btn" disabled>下一页</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.pagination{display:flex;justify-content:space-between;align-items:center;margin-top:16px;padding-top:16px;border-top:1px solid #f0f0f0}
.pagination-info{font-size:13px;color:#999}
.pagination-buttons{display:flex;gap:8px}
.page-btn{padding:6px 12px;border:1px solid #d9d9d9;background:#fff;border-radius:4px;font-size:13px;cursor:pointer;transition:all .2s}
.page-btn:hover:not(:disabled){border-color:#1890ff;color:#1890ff}
.page-btn.active{background:#1890ff;border-color:#1890ff;color:#fff}
.page-btn:disabled{color:#d9d9d9;cursor:not-allowed}
.btn{display:inline-flex;align-items:center;justify-content:center;padding:8px 16px;border-radius:6px;font-size:14px;font-weight:500;border:none;cursor:pointer;transition:all .2s;white-space:nowrap}
.btn-sm{padding:6px 12px;font-size:13px}
.btn-primary{background:#1890ff;color:#fff}.btn-primary:hover{background:#40a9ff}
.data-table{width:100%;border-collapse:collapse;font-size:14px;table-layout:fixed}
.data-table th,.data-table td{padding:10px 12px;border-bottom:1px solid #f0f0f0;box-sizing:border-box}
.data-table th{background:var(--bg);font-weight:600;color:#555;border-bottom:2px solid var(--border);text-align:left}
.data-table td{color:#333;text-align:left}
.data-table tbody tr:hover{background:#f5f7fa}
.col-check{width:40px;text-align:center}.col-id{width:60px;text-align:center}.col-date{width:110px;text-align:center}.col-num{width:80px;text-align:center}.col-action{width:100px;text-align:right}
.data-table th.text,.data-table td.text{text-align:left}
</style>

<script setup>
import { ref } from 'vue'

const activeTab = ref('tab1')

const hfishData = ref([])

const attackerData = [
  { id: '1', ip: '192.168.1.100', location: '广东 深圳', first: '2024-01-15', last: '2024-06-01', count: 128 },
  { id: '2', ip: '10.0.0.50', location: '北京 朝阳', first: '2024-02-20', last: '2024-06-01', count: 86 },
  { id: '3', ip: '172.16.88.25', location: '上海浦东', first: '2024-03-10', last: '2024-05-28', count: 54 },
  { id: '4', ip: '203.0.113.10', location: '美国 加州', first: '2024-04-05', last: '2024-05-15', count: 32 },
  { id: '5', ip: '198.168.55.88', location: '英国 伦敦', first: '2024-05-12', last: '2024-06-01', count: 18 },
]

// 后续通过API获取HFish数据
// onMounted(async () => {
//   const res = await fetch('...')
//   hfishData.value = await res.json()
// })
</script>