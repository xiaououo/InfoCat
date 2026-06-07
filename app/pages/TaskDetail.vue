<template>
  <div class="content-wrapper">
    <div class="content">
      <div class="tab-bar">
        <div class="tab" :class="{ active: activeTab === 'ip-info' }" @click="activeTab = 'ip-info'">服务器信息</div>
        <div class="tab" :class="{ active: activeTab === 'map-view' }" @click="activeTab = 'map-view'">地图展示</div>
        <div class="tab" :class="{ active: activeTab === 'rdns-view' }" @click="activeTab = 'rdns-view'">反向域名解析</div>
        <div class="tab" :class="{ active: activeTab === 'domain-info' }" @click="activeTab = 'domain-info'">域名信息</div>
        <div class="tab" :class="{ active: activeTab === 'domain-history' }" @click="activeTab = 'domain-history'">域名历史解析</div>
        <div class="tab" :class="{ active: activeTab === 'nmap-info' }" @click="activeTab = 'nmap-info'">服务信息（nmap）</div>
        <div class="tab" :class="{ active: activeTab === 'data-operation' }" @click="activeTab = 'data-operation'">数据操作</div>
      </div>
      <div class="tab-content-wrapper">
        <div class="tab-content" :class="{ active: activeTab === 'ip-info' }">
          <div class="result-container">
            <div class="result-card">
              <div class="result-title">IP基本信息</div>
              <div class="info-grid">
                <div class="info-item"><span class="info-label">IP地址</span><span class="info-value highlight">220.172.128.18</span></div>
                <div class="info-item"><span class="info-label">国家/地区</span><span class="info-value">中国 (CN)</span></div>
                <div class="info-item"><span class="info-label">省份/州</span><span class="info-value">广东省</span></div>
                <div class="info-item"><span class="info-label">城市</span><span class="info-value">深圳市</span></div>
                <div class="info-item"><span class="info-label">运营商</span><span class="info-value">中国电信股份有限公司</span></div>
                <div class="info-item"><span class="info-label">组织/公司</span><span class="info-value">Chinanet Guangdong Province Network</span></div>
                <div class="info-item"><span class="info-label">时区</span><span class="info-value">Asia/Shanghai (UTC+8)</span></div>
                <div class="info-item"><span class="info-label">AS号</span><span class="info-value">AS134768 Chinanet</span></div>
              </div>
            </div>
          </div>
        </div>
        <div class="tab-content" :class="{ active: activeTab === 'map-view' }">
          <div class="map-container"><iframe src="https://map.baidu.com/?lat=22.5435&lng=114.0579&l=15" width="100%" height="100%" frameborder="0" allowfullscreen></iframe></div>
        </div>
        <div class="tab-content" :class="{ active: activeTab === 'rdns-view' }">
          <div class="result-container">
            <div class="result-title" style="margin-bottom:16px">反向域名解析结果 (PTR记录)</div>
            <ul class="rdns-list">
              <li class="rdns-item"><div class="rdns-icon">18</div><div class="rdns-value">18.128.172.220.in-addr.arpa</div><div class="rdns-type">PTR</div></li>
              <li class="rdns-item"><div class="rdns-icon">18</div><div class="rdns-value">static.220.172.128.18.clients.your-server.de</div><div class="rdns-type">PTR</div></li>
            </ul>
            <div class="result-card" style="margin-top:16px">
              <div class="result-title">详细信息</div>
              <div class="info-grid">
                <div class="info-item"><span class="info-label">查询IP</span><span class="info-value">220.172.128.18</span></div>
                <div class="info-item"><span class="info-label">主hostname</span><span class="info-value">18.128.172.220.in-addr.arpa</span></div>
                <div class="info-item"><span class="info-label">解析状态</span><span class="info-value highlight">解析成功</span></div>
                <div class="info-item"><span class="info-label">TTL</span><span class="info-value">3600 秒</span></div>
              </div>
            </div>
          </div>
        </div>
        <div class="tab-content" :class="{ active: activeTab === 'domain-info' }">
          <div class="result-container">
            <div class="result-card">
              <div class="result-title">域名解析信息 - example.com</div>
              <div class="info-grid">
                <div class="info-item"><span class="info-label">主域名</span><span class="info-value highlight">example.com</span></div>
                <div class="info-item"><span class="info-label">注册商</span><span class="info-value">GoDaddy.com LLC</span></div>
                <div class="info-item"><span class="info-label">注册时间</span><span class="info-value">1995-08-14</span></div>
                <div class="info-item"><span class="info-label">到期时间</span><span class="info-value">2026-08-13</span></div>
                <div class="info-item"><span class="info-label">DNS服务器</span><span class="info-value">a.iana-servers.net</span></div>
                <div class="info-item"><span class="info-label">域名状态</span><span class="info-value highlight">正常 (ok)</span></div>
              </div>
            </div>
            <div class="result-card" style="margin-top:16px">
              <div class="result-title">DNS解析记录</div>
              <table class="data-table">
                <thead><tr><th>主机记录</th><th>记录类型</th><th>记录值</th><th>TTL</th></tr></thead>
                <tbody>
                  <tr><td>@</td><td><span class="tag tag-a">A</span></td><td>220.172.128.18</td><td>3600</td></tr>
                  <tr><td>www</td><td><span class="tag tag-cname">CNAME</span></td><td>example.com</td><td>3600</td></tr>
                  <tr><td>mail</td><td><span class="tag tag-a">A</span></td><td>220.172.128.20</td><td>3600</td></tr>
                  <tr><td>ftp</td><td><span class="tag tag-cname">CNAME</span></td><td>example.com</td><td>3600</td></tr>
                  <tr><td>@</td><td><span class="tag tag-mx">MX</span></td><td>10 mail.example.com</td><td>3600</td></tr>
                </tbody>
              </table>
            </div>
            <div class="result-card" style="margin-top:16px">
              <div class="result-title">邮箱服务器 (MX)</div>
              <div class="mx-list">
                <div class="mx-item"><span class="mx-priority">10</span><span class="mx-server">mail.example.com</span><span class="tag tag-success">生效中</span></div>
                <div class="mx-item"><span class="mx-priority">20</span><span class="mx-server">backup-mail.example.com</span><span class="tag">备用</span></div>
              </div>
            </div>
          </div>
        </div>
        <div class="tab-content" :class="{ active: activeTab === 'domain-history' }">
          <div class="result-container">
            <div class="result-card">
              <div class="result-title">域名历史解析记录</div>
              <div class="info-grid">
                <div class="info-item"><span class="info-label">查询域名</span><span class="info-value highlight">example.com</span></div>
                <div class="info-item"><span class="info-label">解析记录数</span><span class="info-value">12 条</span></div>
                <div class="info-item"><span class="info-label">最早记录</span><span class="info-value">2020-01-15</span></div>
                <div class="info-item"><span class="info-label">最新记录</span><span class="info-value">2024-06-01</span></div>
              </div>
            </div>
            <div class="result-card" style="margin-top:16px">
              <div class="result-title">IP变更记录</div>
              <table class="data-table">
                <thead><tr><th>时间</th><th>IP</th><th>TTL</th><th>运营商</th></tr></thead>
                <tbody>
                  <tr><td>2024-06-01</td><td><span class="port-num">220.172.128.18</span></td><td>3600</td><td>中国电信</td></tr>
                  <tr><td>2023-03-15</td><td><span class="port-num">192.168.1.100</span></td><td>3600</td><td>中国电信</td></tr>
                  <tr><td>2022-08-20</td><td><span class="port-num">172.16.88.55</span></td><td>7200</td><td>阿里云</td></tr>
                  <tr><td>2021-12-01</td><td><span class="port-num">10.0.0.25</span></td><td>3600</td><td>阿里云</td></tr>
                  <tr><td>2020-06-18</td><td><span class="port-num">203.0.113.10</span></td><td>86400</td><td>Cloudflare</td></tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
        <div class="tab-content" :class="{ active: activeTab === 'nmap-info' }">
          <div class="result-container">
            <div class="result-card">
              <div class="result-title">Nmap扫描结果 - 220.172.128.18</div>
              <div class="summary-box">
                <div class="summary-item"><span class="summary-label">扫描状态</span><span class="summary-value success">开放</span></div>
                <div class="summary-item"><span class="summary-label">开放端口</span><span class="summary-value highlight">4 个</span></div>
                <div class="summary-item"><span class="summary-label">扫描时间</span><span class="summary-value">2024-01-15 14:32:18</span></div>
              </div>
            </div>
            <div class="result-card" style="margin-top:16px">
              <div class="result-title">端口详情</div>
              <table class="data-table">
                <thead><tr><th>端口</th><th>协议</th><th>状态</th><th>服务</th><th>版本</th><th>产品</th></tr></thead>
                <tbody>
                  <tr><td><span class="port-num">22</span></td><td>tcp</td><td><span class="tag tag-success">开放</span></td><td>ssh</td><td>OpenSSH 7.4</td><td>OpenSSH</td></tr>
                  <tr><td><span class="port-num">80</span></td><td>tcp</td><td><span class="tag tag-success">开放</span></td><td>http</td><td>Apache/2.4.6</td><td>Apache httpd</td></tr>
                  <tr><td><span class="port-num">443</span></td><td>tcp</td><td><span class="tag tag-success">开放</span></td><td>https</td><td>nginx/1.20.1</td><td>nginx</td></tr>
                  <tr><td><span class="port-num">3306</span></td><td>tcp</td><td><span class="tag tag-success">开放</span></td><td>mysql</td><td>5.7.36</td><td>MySQL</td></tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
        <div class="tab-content" :class="{ active: activeTab === 'data-operation' }">
          <div class="result-container">
            <div class="result-card">
              <div class="result-title">数据操作</div>
              <div class="operation-buttons">
                <button class="btn btn-primary" @click="exportData">导出</button>
                <button class="btn btn-danger" @click="deleteData">删除</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
:root{--blue:#1890ff;--green:#52c41a;--red:#ff4d4f;--yellow:#faad14;--bg:#fafafa;--border:#e8e8e8}
.result-container{background:var(--bg);border-radius:8px;padding:24px;min-height:200px}
.result-card{background:#fff;border-radius:8px;padding:20px;box-shadow:0 2px 8px rgba(0,0,0,.06)}
.result-title{font-size:16px;font-weight:600;color:#333;margin-bottom:16px;padding-bottom:12px;border-bottom:1px solid var(--border)}
.info-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:16px}
.info-item{display:flex;padding:12px 0;border-bottom:1px solid #f5f5f5}
.info-item:last-child{border-bottom:none}
.info-label{width:100px;color:#666;font-size:14px;flex-shrink:0}
.info-value{flex:1;color:#333;font-size:14px;word-break:break-all}
.info-value.highlight{color:var(--blue);font-weight:500}
.map-container{width:100%;height:calc(100vh - 200px);background:var(--bg)}
.rdns-list{list-style:none}
.rdns-item{display:flex;align-items:center;gap:12px;padding:12px 16px;background:#fff;border-radius:6px;margin-bottom:8px}
.rdns-item:last-child{margin-bottom:0}
.rdns-icon{width:32px;height:32px;background:#e6f7ff;border-radius:50%;display:flex;align-items:center;justify-content:center;color:var(--blue);font-size:14px}
.rdns-value{flex:1;color:#333;font-size:14px;word-break:break-all}
.rdns-type{padding:4px 12px;background:#f5f5f5;border-radius:4px;font-size:12px;color:#666}
.data-table{width:100%;border-collapse:collapse;font-size:14px}
.data-table th,.data-table td{padding:12px 16px;border-bottom:1px solid #f0f0f0;text-align:left}
.data-table th{background:var(--bg);font-weight:600;color:#555;border-bottom:2px solid var(--border)}
.data-table td{color:#333}
.data-table tbody tr:hover{background:#f5f7fa}
.port-num{font-weight:600;color:var(--blue)}
.tag{display:inline-block;padding:2px 8px;border-radius:4px;font-size:12px;font-weight:500}
.tag-a{background:#e6f7ff;color:var(--blue)}
.tag-cname{background:#fff7e6;color:var(--yellow)}
.tag-mx{background:#fff1f0;color:var(--red)}
.tag-success{background:#f6ffed;color:var(--green)}
.summary-box{display:flex;gap:24px;flex-wrap:wrap}
.summary-item{display:flex;align-items:center;gap:12px;padding:12px 20px;background:#f5f5f5;border-radius:8px}
.summary-label{color:#666;font-size:14px}
.summary-value{color:#333;font-size:14px;font-weight:500}
.summary-value.success{color:var(--green)}
.summary-value.highlight{color:var(--blue)}
.mx-list{display:flex;flex-direction:column;gap:8px}
.mx-item{display:flex;align-items:center;gap:16px;padding:12px 16px;background:#fafafa;border-radius:6px}
.mx-priority{width:32px;height:32px;background:#e6f7ff;color:var(--blue);border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:600;font-size:14px}
.mx-server{flex:1;color:#333;font-size:14px}
.operation-buttons{display:flex;gap:12px;flex-wrap:wrap;margin-top:20px}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:10px 24px;border-radius:6px;font-size:14px;font-weight:500;border:none;cursor:pointer;transition:all .2s}
.btn-primary{background:var(--blue);color:#fff}
.btn-primary:hover{background:#40a9ff}
.btn-danger{background:var(--red);color:#fff}
.btn-danger:hover{background:#ff7875}
</style>

<script setup>
import { ref } from 'vue'

const activeTab = ref('ip-info')

function exportData() {
  // 后续接入API
}
function deleteData() {
  // 后续接入API
}
</script>