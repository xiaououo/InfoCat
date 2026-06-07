<template>
  <div class="content-wrapper">
    <div class="agent-container">
      <div class="agent-main">
        <div class="agent-header">
          <div class="model-selector">
            <span class="model-name">智能体(Agent)</span>
          </div>
        </div>
        <div class="agent-messages" id="agentMessages" ref="agentMessagesRef">
          <div class="message-wrapper user-message">
            <div class="message-avatar">U</div>
            <div class="message-bubble">
              <div class="message-content">帮我查询220.172.128.18这个IP的详细信息</div>
              <div class="message-time">14:32</div>
            </div>
          </div>
          <div class="message-wrapper ai-message">
            <div class="message-avatar">AI</div>
            <div class="message-bubble">
              <div class="message-reasoning">
                <div class="reasoning-header">
                  <span class="reasoning-icon">
                    <svg viewBox="0 0 24 24" width="14" height="14" fill="#1890ff">
                      <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1 17.93c-3.95-.49-7-3.85-7-7.93 0-.62.08-1.21.21-1.79L9 15v1c0 1.1.9 2 2 2v1.93zm6.9-2.54c-.26-.81-1-1.39-1.9-1.39h-1v-3c0-.55-.45-1-1-1H8v-2h2c.55 0 1-.45 1-1V7h2c1.1 0 2-.9 2-2v-.41c2.93 1.19 5 4.06 5 7.41 0 2.08-.8 3.97-2.1 5.39z"/>
                    </svg>
                  </span>
                  <span>思考中...</span>
                </div>
                <div class="reasoning-content">
                  <p>接收用户请求：查询IP 220.172.128.18 的详细信息</p>
                  <p>调用IP数据库进行地理位置查询</p>
                  <p>检索到该IP属于中国电信，位置在广东省深圳市</p>
                </div>
              </div>
              <div class="message-response">
                <p>根据查询结果，该IP的详细信息如下：</p>
                <table class="info-table">
                  <tbody>
                  <tr><td>IP地址</td><td>220.172.128.18</td></tr>
                  <tr><td>国家/地区</td><td>中国 广东省 深圳市</td></tr>
                  <tr><td>运营商</td><td>中国电信</td></tr>
                  <tr><td>经纬度</td><td>22.5435, 114.0579</td></tr>
                  <tr><td>AS号</td><td>AS4134</td></tr>
                  <tr><td>时区</td><td>Asia/Shanghai (UTC+8)</td></tr>
                  </tbody>
                </table>
              </div>
              <div class="message-tool">
                <div class="tool-tag">🌐 IP查询</div>
                <div class="tool-time">耗时 1.2s</div>
              </div>
              <div class="message-time">14:32</div>
            </div>
          </div>
        </div>
        <div class="agent-input-wrapper">
          <div class="agent-input-container">
            <textarea v-model="agentInput" class="agent-input" placeholder="输入问题..." rows="1" @keydown.enter.prevent="submitMessage"></textarea>
            <button class="submit-btn" @click="submitMessage">
              <svg viewBox="0 0 24 24" width="20" height="20" fill="#fff">
                <path d="M2.01 21L23 12 2.01 3 2 10l15 2-15 2z"/>
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.agent-container {
  display: flex;
  height: calc(100vh - 120px);
  background: #fff;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}
.logo-icon {
  width: 36px;
  height: 36px;
  background: linear-gradient(135deg, #1890ff, #69c0ff);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 12px;
  font-weight: 600;
}
.logo-text {
  font-size: 16px;
  font-weight: 600;
  color: #333;
}
.new-chat-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  width: 100%;
  padding: 10px;
  background: #1890ff;
  border: none;
  border-radius: 6px;
  color: #fff;
  font-size: 14px;
  cursor: pointer;
  transition: background 0.2s;
}
.new-chat-btn:hover {
  background: #40a9ff;
}
.chat-history {
  flex: 1;
  margin-top: 20px;
  overflow-y: auto;
}
.history-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 12px;
  border-radius: 6px;
  color: #666;
  cursor: pointer;
  transition: all 0.2s;
  margin-bottom: 4px;
}
.history-item:hover {
  background: #e6f7ff;
  color: #1890ff;
}
.history-item.active {
  background: #e6f7ff;
  color: #1890ff;
}
.history-icon {
  font-size: 8px;
}
.history-text {
  font-size: 14px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.agent-main {
  flex: 1;
  display: flex;
  flex-direction: column;
}
.agent-header {
  padding: 16px 24px;
  border-bottom: 1px solid #e8e8e8;
  display: flex;
  justify-content: center;
  background: #fafafa;
}
.model-selector {
  display: flex;
  align-items: center;
  gap: 8px;
}
.model-name {
  color: #333;
  font-size: 14px;
  font-weight: 500;
}
.agent-messages {
  flex: 1;
  min-height: 0;
  overflow-y: auto;
  padding: 24px;
  background: #fff;
}
.message-wrapper {
  display: flex;
  gap: 10px;
  margin-bottom: 24px;
  max-width: 800px;
}
.user-message {
  margin-left: auto;
  flex-direction: row-reverse;
}
.ai-message .message-avatar {
  width: 36px;
  height: 36px;
  background: linear-gradient(135deg, #1890ff, #69c0ff);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 11px;
  font-weight: 600;
  flex-shrink: 0;
}
.user-message .message-avatar {
  width: 36px;
  height: 36px;
  background: #f5f5f5;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #666;
  font-size: 12px;
  font-weight: 600;
  flex-shrink: 0;
}
.message-bubble {
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.message-content {
  padding: 12px 16px;
  background: #f5f5f5;
  border-radius: 12px 12px 12px 4px;
  color: #333;
  font-size: 14px;
  line-height: 1.6;
  word-break: break-word;
  max-width: 80%;
}
.user-message .message-content {
  background: #1890ff;
  color: #fff;
  border-radius: 12px 12px 4px 12px;
  max-width: 80%;
}
.message-time {
  font-size: 11px;
  color: #999;
  margin-top: 6px;
}
.user-message .message-time {
  text-align: right;
}
.message-reasoning {
  background: #f5f7fa;
  border: 1px solid #e8e8e8;
  border-radius: 8px;
  padding: 14px 16px;
  margin-bottom: 16px;
}
.reasoning-header {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #666;
  font-size: 13px;
  margin-bottom: 10px;
}
.reasoning-icon {
  display: flex;
  align-items: center;
}
.reasoning-content p {
  color: #888;
  font-size: 13px;
  line-height: 1.6;
  margin: 0 0 6px 0;
  padding-left: 22px;
}
.reasoning-content p:last-child {
  margin-bottom: 0;
}
.message-response {
  padding: 12px 16px;
  background: #f5f5f5;
  border-radius: 12px 12px 12px 4px;
  color: #333;
  font-size: 14px;
  line-height: 1.7;
}
.message-response p {
  margin: 0 0 12px 0;
}
.message-response p:last-child {
  margin-bottom: 0;
}
.info-table {
  width: 100%;
  border-collapse: collapse;
  background: #fafafa;
  border-radius: 8px;
  overflow: hidden;
  border: 1px solid #e8e8e8;
}
.info-table td {
  padding: 10px 14px;
  border-bottom: 1px solid #f0f0f0;
  color: #333;
}
.info-table td:first-child {
  color: #666;
  width: 120px;
  background: #f5f7fa;
}
.info-table tr:last-child td {
  border-bottom: none;
}
.message-tool {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 12px;
  padding-top: 12px;
  border-top: 1px solid #f0f0f0;
}
.tool-tag {
  padding: 4px 10px;
  background: #e6f7ff;
  border-radius: 4px;
  font-size: 12px;
  color: #1890ff;
}
.tool-time {
  font-size: 12px;
  color: #999;
}
.agent-input-wrapper {
  flex-shrink: 0;
  padding: 16px 24px 24px;
  border-top: 1px solid #e8e8e8;
  background: #fafafa;
}
.agent-input-container {
  display: flex;
  gap: 12px;
  align-items: stretch;
  background: #fff;
  border: 1px solid #d9d9d9;
  border-radius: 8px;
  padding: 8px 8px 8px 16px;
}
.agent-input-container:focus-within {
  border-color: #1890ff;
  box-shadow: 0 0 0 2px rgba(24,144,255,0.1);
}
.agent-input {
  flex: 1;
  background: transparent;
  border: none;
  outline: none;
  color: #333;
  font-size: 14px;
  resize: none;
  max-height: 120px;
  line-height: 1.5;
}
.agent-input::placeholder {
  color: #bfbfbf;
}
.submit-btn {
  width: 40px;
  height: 40px;
  background: #1890ff;
  border: none;
  border-radius: 6px;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.2s;
  flex-shrink: 0;
}
.submit-btn:hover {
  background: #40a9ff;
}
</style>

<script setup>
import { ref } from 'vue'

const agentInput = ref('')
const agentMessagesRef = ref(null)

function submitMessage() {
  if (!agentInput.value.trim()) return
  // 后续接入API
  agentInput.value = ''
}
</script>