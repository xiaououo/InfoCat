<template>
  <div class="content-wrapper">
    <div class="tab-bar">
      <div class="tab active" data-content="tab1" @click="activeTab = 'tab1'" :class="{ active: activeTab === 'tab1' }">FOFA 搜索</div>
      <div class="tab" data-content="tab2" @click="activeTab = 'tab2'" :class="{ active: activeTab === 'tab2' }">FOFA缓存搜索</div>
    </div>
    <div class="tab-content-wrapper">
      <div class="tab-content" :class="{ active: activeTab === 'tab1' }">
        <div class="fofa-container">
          <div class="card search-card">
            <div class="search-header">
              <h3 class="card-title">FOFA 搜索</h3>
              <div class="search-box">
                <input type="text" v-model="fofaQuery" class="search-input" placeholder="输入 FOFA 查询语法，如：protocol=ftp and country=CN" @keypress.enter="doSearch">
                <button class="search-btn" @click="doSearch">搜索</button>
              </div>
            </div>
            <div class="search-filters">
              <div class="filter-row">
                <span class="filter-label">快速筛选：</span>
                <button class="filter-btn" @click="addFilter('protocol=http')">HTTP</button>
                <button class="filter-btn" @click="addFilter('protocol=https')">HTTPS</button>
                <button class="filter-btn" @click="addFilter('port=80')">端口80</button>
                <button class="filter-btn" @click="addFilter('port=443')">端口443</button>
              </div>
            </div>
          </div>

          <div class="card results-card">
            <div class="results-header">
              <h3 class="card-title">搜索结果</h3>
            </div>
            <table class="results-table">
              <thead>
                <tr>
                  <th>IP</th>
                  <th>端口</th>
                  <th>协议</th>
                  <th>国家/地区</th>
                  <th>组织</th>
                  <th>标题</th>
                  <th>任务</th>
                  <th>操作</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>123.45.67.89</td>
                  <td>80</td>
                  <td><span class="protocol http">HTTP</span></td>
                  <td>🇨🇳 CN</td>
                  <td>Tencent Cloud</td>
                  <td>Welcome to Nginx</td>
                  <td><button class="action-btn">添加至任务</button></td>
                  <td><button class="action-btn">查看详情</button></td>
                </tr>
                <tr>
                  <td>98.765.43.210</td>
                  <td>443</td>
                  <td><span class="protocol https">HTTPS</span></td>
                  <td>🇨🇳 CN</td>
                  <td>Alibaba Cloud</td>
                  <td>Apache Tomcat</td>
                  <td><button class="action-btn">添加至任务</button></td>
                  <td><button class="action-btn">查看详情</button></td>
                </tr>
              </tbody>
            </table>
            <div class="pagination">
              <span class="pagination-info">共 4 条</span>
              <div class="pagination-right">
                <div class="pagination-buttons">
                  <button class="page-btn" disabled>上一页</button>
                  <button class="page-btn active">1</button>
                  <button class="page-btn" disabled>下一页</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="tab-content" :class="{ active: activeTab === 'tab2' }">
        <div class="fofa-container">
          <div class="card results-card">
            <div class="results-header">
              <h3 class="card-title">缓存搜索</h3>
              <div class="cache-controls">
                <input type="text" v-model="cacheName" class="cache-input" placeholder="模糊搜索">
                <button class="cache-btn" @click="saveCache">搜索缓存</button>
                <button class="cache-btn clear" @click="clearCache">清理缓存</button>
              </div>
            </div>
            <table class="results-table">
              <thead>
                <tr>
                  <th>IP</th>
                  <th>端口</th>
                  <th>协议</th>
                  <th>国家/地区</th>
                  <th>组织</th>
                  <th>标题</th>
                  <th>操作</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>192.168.1.1</td>
                  <td>8080</td>
                  <td><span class="protocol http">HTTP</span></td>
                  <td>🇨🇳 CN</td>
                  <td>Huawei</td>
                  <td>Apache</td>
                  <td><button class="action-btn">查看详情</button></td>
                </tr>
                <tr>
                  <td>192.168.1.2</td>
                  <td>3306</td>
                  <td><span class="protocol https">MySQL</span></td>
                  <td>🇨🇳 CN</td>
                  <td>Alibaba</td>
                  <td>MySQL 5.5</td>
                  <td><button class="action-btn">查看详情</button></td>
                </tr>
                <tr>
                  <td>192.168.1.3</td>
                  <td>22</td>
                  <td><span class="protocol ssh">SSH</span></td>
                  <td>🇺🇸 US</td>
                  <td>AWS</td>
                  <td>OpenSSH</td>
                  <td><button class="action-btn">查看详情</button></td>
                </tr>
              </tbody>
            </table>
            <div class="pagination">
              <span class="pagination-info">共 3 条</span>
              <div class="pagination-right">
                <div class="pagination-buttons">
                  <button class="page-btn" disabled>上一页</button>
                  <button class="page-btn active">1</button>
                  <button class="page-btn" disabled>下一页</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fofa-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  background: #fff;
  padding: 20px;
  border-radius: 8px;
}
.search-card {
  padding: 20px;
}
.search-header {
  margin-bottom: 16px;
}
.search-box {
  display: flex;
  gap: 12px;
  margin-top: 12px;
}
.search-input {
  flex: 1;
  padding: 10px 14px;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  font-size: 14px;
}
.search-input:focus {
  border-color: #1890ff;
  outline: none;
  box-shadow: 0 0 0 2px rgba(24,144,255,0.2);
}
.search-filters {
  padding-top: 12px;
  border-top: 1px solid #f0f0f0;
}
.filter-row {
  display: flex;
  align-items: center;
  gap: 8px;
  flex-wrap: wrap;
}
.filter-label {
  font-size: 14px;
  color: #666;
}
.filter-btn {
  padding: 4px 12px;
  background: #f5f5f5;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
  transition: all 0.2s;
}
.filter-btn:hover {
  background: #e6f7ff;
  border-color: #1890ff;
  color: #1890ff;
}
.results-card {
  padding: 20px;
}
.results-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}
.cache-controls {
  display: flex;
  gap: 8px;
  align-items: center;
}
.cache-input {
  padding: 6px 10px;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  font-size: 13px;
  width: 140px;
}
.cache-input:focus {
  border-color: #1890ff;
  outline: none;
}
.cache-btn {
  padding: 6px 12px;
  background: #1890ff;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 13px;
  cursor: pointer;
  transition: all 0.2s;
}
.cache-btn:hover {
  background: #40a9ff;
}
.cache-btn.clear {
  background: #ff4d4f;
}
.cache-btn.clear:hover {
  background: #ff7875;
}
.results-table {
  width: 100%;
  border-collapse: collapse;
}
.results-table th {
  text-align: left;
  padding: 12px 8px;
  background: #fafafa;
  font-weight: 600;
  font-size: 13px;
  color: #333;
  border-bottom: 1px solid #f0f0f0;
}
.results-table td {
  padding: 12px 8px;
  border-bottom: 1px solid #f0f0f0;
  font-size: 13px;
  color: #333;
}
.results-table tr:hover {
  background: #fafafa;
}
.protocol {
  padding: 2px 6px;
  border-radius: 3px;
  font-size: 11px;
  font-weight: 500;
}
.protocol.http { background: #e6f7ff; color: #1890ff; }
.protocol.https { background: #f6ffed; color: #52c41a; }
.protocol.ssh { background: #fff7e6; color: #faad14; }
.action-btn {
  padding: 4px 12px;
  background: #1890ff;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
}
.action-btn:hover {
  background: #40a9ff;
}
.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 16px;
  padding-top: 16px;
  border-top: 1px solid #f0f0f0;
}
.pagination-info {
  font-size: 13px;
  color: #999;
}
.pagination-buttons {
  display: flex;
  gap: 8px;
}
.page-btn {
  padding: 6px 12px;
  border: 1px solid #d9d9d9;
  background: #fff;
  border-radius: 4px;
  font-size: 13px;
  cursor: pointer;
  transition: all 0.2s;
}
.page-btn:hover:not(:disabled) {
  border-color: #1890ff;
  color: #1890ff;
}
.page-btn.active {
  background: #1890ff;
  border-color: #1890ff;
  color: #fff;
}
.page-btn:disabled {
  color: #d9d9d9;
  cursor: not-allowed;
}
</style>

<script setup>
import { ref } from 'vue'

const activeTab = ref('tab1')
const fofaQuery = ref('')
const cacheName = ref('')

function doSearch() {
  if (!fofaQuery.value) return
  // 后续接入API
}
function addFilter(filter) {
  if (fofaQuery.value) {
    fofaQuery.value += ' && ' + filter
  } else {
    fofaQuery.value = filter
  }
}
function saveCache() {
  // 后续接入API
}
function clearCache() {
  cacheName.value = ''
  // 后续接入API
}
</script>