<template>
  <div class="content-wrapper">
    <div class="tab-bar">
      <div class="tab" :class="{ active: activeTab === 'fofa' }" @click="activeTab = 'fofa'">FOFA 配置</div>
      <div class="tab" :class="{ active: activeTab === 'hfish' }" @click="activeTab = 'hfish'">HFish 配置</div>
    </div>
    <div class="tab-content-wrapper">
      <div class="tab-content" :class="{ active: activeTab === 'fofa' }">
        <div class="form-card">
          <div class="form-row"><label>Email</label><input type="text" v-model="fofaEmail" placeholder="FOFA Email"></div>
          <div class="form-row"><label>API Key</label><input type="password" v-model="fofaKey" placeholder="FOFA API Key"></div>
          <div class="form-row"><label>搜索数量</label><input type="number" v-model="fofaLimit"></div>
          <div class="form-btns"><button class="btn btn-primary" @click="saveFofa">保存</button><button class="btn btn-default" @click="testFofa">测试连接</button></div>
        </div>
      </div>
      <div class="tab-content" :class="{ active: activeTab === 'hfish' }">
        <div class="form-card">
          <div class="form-row"><label>IP地址</label><input type="text" v-model="hfishIP" placeholder="HFish 服务器 IP"></div>
          <div class="form-row"><label>API Key</label><input type="password" v-model="hfishKey" placeholder="HFish API Key"></div>
          <div class="form-row"><label>端口</label><input type="number" v-model="hfishPort"></div>
          <div class="form-btns"><button class="btn btn-primary" @click="saveHfish">保存</button><button class="btn btn-default" @click="testHfish">测试连接</button></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.form-card{background:#fff;border-radius:8px;padding:24px;box-shadow:0 2px 8px rgba(0,0,0,.06);max-width:600px}
.form-row{margin-bottom:20px}
.form-row label{display:block;font-size:14px;color:#666;margin-bottom:8px}
.form-row input{width:100%;padding:10px 12px;border:1px solid #d9d9d9;border-radius:6px;font-size:14px;box-sizing:border-box}
.form-row input:focus{border-color:#1890ff;outline:none}
.form-btns{display:flex;gap:12px;margin-top:28px;flex-wrap:wrap}
.btn{display:inline-flex;align-items:center;justify-content:center;padding:10px 20px;border-radius:6px;font-size:14px;font-weight:500;border:none;cursor:pointer;transition:all .2s;white-space:nowrap;text-align:center}
.btn-primary{background:#1890ff;color:#fff}.btn-primary:hover{background:#40a9ff}
.btn-default{background:#fff;color:#333;border:1px solid #d9d9d9}.btn-default:hover{color:#1890ff;border-color:#1890ff}
</style>

<script setup>
import { ref } from 'vue'

const activeTab = ref('fofa')
const fofaEmail = ref('')
const fofaKey = ref('')
const fofaLimit = ref(100)
const hfishIP = ref('')
const hfishKey = ref('')
const hfishPort = ref(8989)

function saveFofa() {
  if (!fofaEmail.value.trim() || !fofaKey.value.trim()) return
  // 后续接入API
}
function testFofa() {
  if (!fofaEmail.value.trim() || !fofaKey.value.trim()) return
  // 后续接入API
}
function saveHfish() {
  if (!hfishIP.value.trim() || !hfishKey.value.trim()) return
  // 后续接入API
}
function testHfish() {
  if (!hfishIP.value.trim() || !hfishKey.value.trim()) return
  // 后续接入API
}
</script>