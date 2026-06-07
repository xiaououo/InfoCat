<template>
  <div class="layout">
    <aside class="sidebar">
      <div class="logo">InfoCat 2.0</div>
      <div class="menu">
        <div
          v-for="item in menuItems"
          :key="item.path"
          class="menu-item"
          :class="{ active: currentPath === item.path }"
        >
          <NuxtLink :to="item.path" class="a">
            <span class="menu-icon"></span>
            <span>{{ item.name }}</span>
          </NuxtLink>
        </div>
      </div>
    </aside>

    <main class="main">
      <header class="navbar">
        <div class="user-box">
          <div class="avatar"></div>
          <div class="username">User</div>
        </div>
      </header>

      <slot />
    </main>
  </div>
</template>

<script setup>
const route = useRoute()

const menuItems = [
  { path: '/', name: '首页' },
  { path: '/FOFA', name: 'FOFA' },
  { path: '/TaskList', name: '任务列表' },
  { path: '/HFish', name: 'HFish' },
  { path: '/Agent', name: '智能体(Agent)' },
  { path: '/Shell', name: '控制终端' },
  { path: '/Settings', name: '系统设置' },
]

const currentPath = computed(() => {
  if (route.path === '/') return '/'
  const seg = route.path.split('/')[1]
  return '/' + seg
})
</script>