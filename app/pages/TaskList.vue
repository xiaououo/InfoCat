<template>
  <div class="content-wrapper">
    <div class="tab-bar">
      <div class="tab" :class="{ active: activeTab === 'tab1' }" @click="activeTab = 'tab1'">任务列表</div>
      <div class="tab" :class="{ active: activeTab === 'tab2' }" @click="activeTab = 'tab2'">任务组</div>
    </div>
    <div class="tab-content-wrapper">
      <div class="tab-content" :class="{ active: activeTab === 'tab1' }">
        <div class="table-toolbar">
          <h3 class="table-title">开始任务</h3>
          <div class="table-toolbar-right">
            <div class="create-task-wrapper">
              <button class="create-task-btn" @click="toggleCreateTask">+ 创建任务</button>
              <div class="create-task-dropdown" :class="{ show: createTaskOpen }">
                <div class="dropdown-item"><label>任务组</label><select v-model="formGroup"><option value="">请选择任务组</option><option value="1">192.168.1.1</option><option value="2">192.168.1.4</option></select></div>
                <div class="dropdown-item"><label>任务名称</label><input type="text" v-model="formName" placeholder="请输入任务名称"></div>
                <div class="dropdown-item"><label>IP地址</label><input type="text" v-model="formIP" placeholder="请输入IP地址"></div>
                <div class="dropdown-footer"><button class="btn btn-primary" @click="createTaskHandle">创建</button><button class="btn btn-default" @click="toggleCreateTask">取消</button></div>
              </div>
            </div>
            <input type="text" class="search-input" placeholder="搜索任务...">
            <button class="search-btn">搜索</button>
          </div>
        </div>
        <table class="data-table">
          <thead>
            <tr>
              <th>任务ID</th>
              <th>任务类型</th>
              <th>任务分组</th>
              <th>任务名称</th>
              <th>IP地址</th>
              <th>任务时间</th>
              <th>互联网服务商</th>
              <th>状态</th>
              <th>操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in taskData" :key="item.id">
              <td>{{ item.id }}</td>
              <td>{{ item.type }}</td>
              <td>{{ item.group }}</td>
              <td>{{ item.name }}</td>
              <td>{{ item.IP }}</td>
              <td>{{ item.Data }}</td>
              <td>{{ item.isp }}</td>
              <td>{{ item.status }}</td>
              <td><NuxtLink :to="'/TaskDetail?id=' + item.id" class="btn btn-primary">查看详情</NuxtLink></td>
            </tr>
          </tbody>
        </table>
        <div class="pagination">
          <span class="pagination-info">共 5 条</span>
          <div class="pagination-right">
            <div class="pagination-buttons">
              <button class="page-btn" disabled>上一页</button>
              <button class="page-btn active">1</button>
              <button class="page-btn" disabled>下一页</button>
            </div>
          </div>
        </div>
      </div>

      <div class="tab-content" :class="{ active: activeTab === 'tab2' }">
        <div class="table-toolbar">
          <h3 class="table-title">任务组列表</h3>
          <div class="table-search">
            <input type="text" class="search-input" placeholder="搜索任务组...">
            <button class="search-btn">搜索</button>
            <button class="search-btn" @click="openCreateModal">+ 创建任务组</button>
          </div>
        </div>
        <table class="data-table">
          <thead>
            <tr>
              <th>任务组ID</th>
              <th>任务组名称</th>
              <th>任务数量</th>
              <th>创建时间</th>
              <th>创建角色</th>
              <th>预览</th>
              <th>操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in groupData" :key="item.id">
              <td>{{ item.id }}</td>
              <td>{{ item.name }}</td>
              <td>{{ item.count }}</td>
              <td>{{ item.create_time }}</td>
              <td>{{ item.create_role }}</td>
              <td><a href="#" class="btn btn-primary">查看详情</a></td>
              <td><a href="#" class="btn btn-danger">删除</a></td>
            </tr>
          </tbody>
        </table>
        <div class="pagination">
          <span class="pagination-info">共 2 条</span>
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

    <div class="modal" :class="{ show: modalOpen }">
      <div class="modal-content">
        <div class="modal-header">
          <h3>创建任务组</h3>
          <span class="modal-close" @click="closeCreateModal">&times;</span>
        </div>
        <div class="modal-body">
          <label>任务组名称</label>
          <input type="text" v-model="groupName" class="search-input" placeholder="请输入任务组名称" style="width: 100%;" @keypress.enter="createGroup">
        </div>
        <div class="modal-footer">
          <button class="search-btn" @click="closeCreateModal">取消</button>
          <button class="search-btn" style="background: #52c41a;" @click="createGroup">创建</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  z-index: 1000;
  justify-content: center;
  align-items: center;
}
.modal.show {
  display: flex;
}
.modal-content {
  background: #fff;
  border-radius: 8px;
  width: 400px;
  max-width: 90%;
  box-shadow: 0 4px 20px rgba(0,0,0,0.15);
}
.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 20px;
  border-bottom: 1px solid #e8e8e8;
}
.modal-header h3 {
  margin: 0;
  font-size: 16px;
  font-weight: 600;
  color: #333;
}
.modal-close {
  font-size: 24px;
  color: #999;
  cursor: pointer;
  line-height: 1;
}
.modal-close:hover {
  color: #333;
}
.modal-body {
  padding: 20px;
}
.modal-body label {
  display: block;
  margin-bottom: 8px;
  font-size: 14px;
  color: #666;
}
.modal-footer {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  padding: 16px 20px;
  border-top: 1px solid #e8e8e8;
}
.btn {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 12px;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.2s;
  text-align: center;
}
.btn-primary {
  background: #1890ff;
  color: #fff;
  border: none;
}
.btn-primary:hover {
  background: #40a9ff;
}
.btn-danger {
  background: #ff4d4f;
  color: #fff;
  border: none;
}
.btn-danger:hover {
  background: #ff7875;
}
.pagination { display: flex; justify-content: space-between; align-items: center; margin-top: 16px; padding-top: 16px; border-top: 1px solid #f0f0f0; }
.pagination-info { font-size: 13px; color: #999; }
.pagination-buttons { display: flex; gap: 8px; }
.page-btn { padding: 6px 12px; border: 1px solid #d9d9d9; background: #fff; border-radius: 4px; font-size: 13px; cursor: pointer; transition: all .2s; }
.page-btn:hover:not(:disabled) { border-color: #1890ff; color: #1890ff; }
.page-btn.active { background: #1890ff; border-color: #1890ff; color: #fff; }
.page-btn:disabled { color: #d9d9d9; cursor: not-allowed; }
.table-toolbar { display: flex; justify-content: space-between; align-items: center; margin-bottom: 16px; }
.table-toolbar-right { display: flex; gap: 12px; align-items: center; }
.create-task-wrapper { position: relative; }
.create-task-btn { padding: 8px 16px; background: #1890ff; color: #fff; border: none; border-radius: 4px; font-size: 14px; cursor: pointer; }
.create-task-btn:hover { background: #40a9ff; }
.create-task-dropdown { display: none; position: absolute; top: 100%; right: 0; margin-top: 8px; background: #fff; border: 1px solid #e8e8e8; border-radius: 8px; box-shadow: 0 4px 20px rgba(0,0,0,0.15); width: 320px; z-index: 100; }
.create-task-dropdown.show { display: block; }
.dropdown-item { padding: 12px 16px; border-bottom: 1px solid #f0f0f0; }
.dropdown-item:last-child { border-bottom: none; }
.dropdown-item label { display: block; margin-bottom: 6px; font-size: 13px; color: #666; }
.dropdown-item input, .dropdown-item select { width: 100%; padding: 8px 12px; border: 1px solid #d9d9d9; border-radius: 4px; font-size: 14px; box-sizing: border-box; }
.dropdown-item input:focus, .dropdown-item select:focus { border-color: #1890ff; outline: none; }
.dropdown-footer { padding: 12px 16px; display: flex; gap: 8px; justify-content: flex-end; background: #fafafa; border-radius: 0 0 8px 8px; }
.btn-default { padding: 8px 16px; background: #fff; color: #333; border: 1px solid #d9d9d9; border-radius: 4px; font-size: 14px; cursor: pointer; }
.btn-default:hover { color: #1890ff; border-color: #1890ff; }
</style>

<script setup>
import { ref } from 'vue'

const activeTab = ref('tab1')
const modalOpen = ref(false)
const createTaskOpen = ref(false)
const groupName = ref('')
const formGroup = ref('')
const formName = ref('')
const formIP = ref('')

const taskData = [
  { id: '1', type: '手动任务', group: '192.168.1.1', name: '美国白宫', IP: '192.168.1.1', Data: '2023-08-01 12:00:00', isp: '阿里云', status: '运行中' },
  { id: '2', type: '手动任务', group: '192.168.1.1', name: '缅甸诈骗', IP: '192.168.1.2', Data: '2023-08-02 12:00:00', isp: '阿里云', status: '运行中' },
  { id: '3', type: '手动任务', group: '192.168.1.1', name: '米哈游用户中心', IP: '192.168.1.3', Data: '2023-08-03 12:00:00', isp: '阿里云', status: '运行中' },
  { id: '4', type: 'AI任务', group: '192.168.1.4', name: 'AD域控服务器', IP: '192.168.1.4', Data: '2023-08-04 12:00:00', isp: '阿里云', status: '运行中' },
  { id: '5', type: 'AI任务', group: '192.168.1.4', name: '澳门赌场', IP: '192.168.1.5', Data: '2023-08-05 12:00:00', isp: '阿里云', status: '运行中' },
]

const groupData = [
  { id: '1', name: '192.168.1.1', count: 3, create_time: '2023-08-01 12:00:00', create_role: '管理员' },
  { id: '2', name: '192.168.1.4', count: 2, create_time: '2023-08-02 12:00:00', create_role: 'AI智能体' },
]

function openCreateModal() {
  modalOpen.value = true
  groupName.value = ''
}
function closeCreateModal() {
  modalOpen.value = false
}
function createGroup() {
  if (!groupName.value.trim()) return
  closeCreateModal()
  // 后续接入API
}
function toggleCreateTask() {
  createTaskOpen.value = !createTaskOpen.value
  if (createTaskOpen.value) {
    formGroup.value = ''
    formName.value = ''
    formIP.value = ''
  }
}
function createTaskHandle() {
  if (!formGroup.value || !formName.value.trim() || !formIP.value.trim()) return
  toggleCreateTask()
  // 后续接入API
}
</script>