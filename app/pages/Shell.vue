<template>
  <div class="content-wrapper">
    <div class="content">
      <div class="terminal-window">
        <div class="terminal-body" ref="terminalBodyRef">
          <div class="output-line">[root@localhost ~]# echo "Welcome to Linux Terminal"</div>
          <div class="output-line">Welcome to Linux Terminal</div>
          <div class="output-line">[root@localhost ~]# uname -a</div>
          <div class="output-line">Linux localhost 5.15.0-101-generic #111 SMP Tue Aug 9 11:12:49 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux</div>
          <div class="output-line">[root@localhost ~]# </div>
        </div>
        <div class="terminal-input-row" @click="focusInput">
          <span class="prompt">[root@localhost ~]# </span>
          <span class="input-text">{{ currentCmd }}</span>
          <span class="cursor"> </span>
        </div>
        <input
          type="text"
          class="terminal-input"
          ref="terminalInputRef"
          v-model="currentCmd"
          autocomplete="off"
          spellcheck="false"
          @keydown.enter="executeCommand"
        >
      </div>
    </div>
  </div>
</template>

<style scoped>
.terminal-window {
  height: 100%;
  background: #fff;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  font-family: 'Courier New', 'Lucida Console', monospace;
  border: 1px solid var(--border);
  position: relative;
}
.terminal-body {
  flex: 1;
  padding: 12px 16px;
  overflow-y: auto;
  color: #000;
  font-size: 14px;
  line-height: 1.5;
  background: #fff;
}
.output-line {
  margin-bottom: 2px;
  white-space: pre-wrap;
  word-break: break-all;
}
.terminal-input-row {
  display: flex;
  align-items: center;
  padding: 8px 16px;
  background: #fff;
  font-size: 14px;
}
.prompt {
  color: #000;
  margin-right: 0;
  white-space: nowrap;
}
.input-text {
  color: #000;
  white-space: pre;
}
.cursor {
  display: inline-block;
  width: 8px;
  height: 14px;
  background: #000;
  animation: blink 1s step-end infinite;
}
@keyframes blink {
  50% { opacity: 0; }
}
.terminal-input {
  position: absolute;
  opacity: 0;
  pointer-events: none;
}
.terminal-body::-webkit-scrollbar {
  width: 12px;
}
.terminal-body::-webkit-scrollbar-track {
  background: #f0f0f0;
}
.terminal-body::-webkit-scrollbar-thumb {
  background: #c0c0c0;
  border: 2px solid #f0f0f0;
}
</style>

<script setup>
import { ref, nextTick, onMounted } from 'vue'

const currentCmd = ref('')
const terminalInputRef = ref(null)
const terminalBodyRef = ref(null)

const commands = {
  'help': '[root@localhost ~]# help\nSupported commands:\n  help    - Show this help message\n  ls      - List directory contents\n  pwd     - Print working directory\n  whoami  - Print current user\n  date    - Print system date\n  clear   - Clear terminal screen\n  echo    - Print text to terminal\n  uname   - Print system information\n  cat     - Concatenate and display files\n  uptime  - Show system uptime\n  ifconfig - Configure network interface',
  'ls': '[root@localhost ~]# ls\nbin   boot  dev  etc  home  lib  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var',
  'pwd': '[root@localhost ~]# pwd\n/root',
  'whoami': '[root@localhost ~]# whoami\nroot',
  'date': `[root@localhost ~]# date\n${new Date().toString().split(' ').slice(0, 5).join(' ')}`,
  'uptime': '[root@localhost ~]# uptime\n ' + new Date().toTimeString().split(' ')[0] + ' up 42 days, 7:23, 3 users, load average: 0.15, 0.12, 0.08',
  'uname': '[root@localhost ~]# uname -a\nLinux localhost 5.15.0-101-generic #111 SMP Tue Aug 9 11:12:49 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux',
  'ifconfig': '[root@localhost ~]# ifconfig\neth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500\n        inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255\n        ether 00:11:22:33:44:55  txqueuelen 1000  (Ethernet)\n        RX packets 12345  bytes 1234567 (1.2 MB)\n        TX packets 6789   bytes 987654 (964.8 KB)\n\nlo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536\n        inet 127.0.0.1  netmask 255.0.0.0\n        loop  txqueuelen 1000  (Local Loopback)'
}

function addOutput(text) {
  const line = document.createElement('div')
  line.className = 'output-line'
  line.textContent = text
  terminalBodyRef.value.appendChild(line)
  terminalBodyRef.value.scrollTop = terminalBodyRef.value.scrollHeight
}

function executeCommand() {
  const cmd = currentCmd.value.trim()
  const parts = cmd.split(' ')
  const command = parts[0].toLowerCase()
  const args = parts.slice(1).join(' ')

  if (command === '') return

  if (command === 'clear') {
    terminalBodyRef.value.innerHTML = ''
    addOutput('')
  } else if (command === 'echo') {
    addOutput('[root@localhost ~]# ' + cmd)
    addOutput(args || '')
  } else if (command === 'cat') {
    addOutput('[root@localhost ~]# ' + cmd)
    if (args) {
      addOutput('cat: ' + args + ': No such file or directory')
    } else {
      addOutput('cat: missing file operand')
    }
  } else if (commands[command] !== undefined) {
    addOutput(commands[command])
  } else {
    addOutput('[root@localhost ~]# ' + cmd)
    addOutput('bash: ' + command + ': command not found')
  }
  addOutput('')
  currentCmd.value = ''
}

function focusInput() {
  terminalInputRef.value?.focus()
}

onMounted(() => {
  terminalInputRef.value?.focus()
})
</script>