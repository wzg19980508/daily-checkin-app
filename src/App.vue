<template>
  <div class="min-h-screen pb-20">
    <!-- 头部 -->
    <header class="bg-gradient-to-r from-blue-500 to-purple-600 text-white p-6 rounded-b-3xl shadow-lg">
      <div class="max-w-md mx-auto">
        <h1 class="text-2xl font-bold">📅 每日打卡</h1>
        <p class="text-blue-100 text-sm mt-1">坚持每一天，成就更好的自己</p>
        
        <!-- 今日日期 -->
        <div class="mt-4 bg-white/20 backdrop-blur-sm rounded-xl p-3">
          <div class="text-center">
            <div class="text-3xl font-bold">{{ currentDate.day }}</div>
            <div class="text-sm">{{ currentDate.weekday }}</div>
          </div>
        </div>
      </div>
    </header>

    <!-- 主内容区 -->
    <main class="max-w-md mx-auto p-4">
      <!-- 当前视图 -->
      <component :is="currentView" :habits="habits" @update:habits="updateHabits" />
    </main>

    <!-- 底部导航 -->
    <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 px-6 py-2 safe-area-bottom">
      <div class="max-w-md mx-auto flex justify-around">
        <button 
          @click="currentView = HomeView"
          :class="['flex flex-col items-center p-2 rounded-xl transition-all', currentView === HomeView ? 'text-blue-500 bg-blue-50' : 'text-gray-400']"
        >
          <span class="text-2xl">🏠</span>
          <span class="text-xs mt-1">首页</span>
        </button>
        
        <button 
          @click="currentView = CalendarView"
          :class="['flex flex-col items-center p-2 rounded-xl transition-all', currentView === CalendarView ? 'text-blue-500 bg-blue-50' : 'text-gray-400']"
        >
          <span class="text-2xl">📆</span>
          <span class="text-xs mt-1">日历</span>
        </button>
        
        <button 
          @click="currentView = StatsView"
          :class="['flex flex-col items-center p-2 rounded-xl transition-all', currentView === StatsView ? 'text-blue-500 bg-blue-50' : 'text-gray-400']"
        >
          <span class="text-2xl">📊</span>
          <span class="text-xs mt-1">统计</span>
        </button>
      </div>
    </nav>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import HomeView from './views/HomeView.vue'
import CalendarView from './views/CalendarView.vue'
import StatsView from './views/StatsView.vue'

// 当前视图
const currentView = ref(HomeView)

// 习惯数据
const habits = ref([
  { id: 1, name: '早起晨跑', icon: '🏃', completed: false, streak: 5 },
  { id: 2, name: '阅读 30 分钟', icon: '📚', completed: false, streak: 12 },
  { id: 3, name: '健康饮食', icon: '🥗', completed: false, streak: 8 },
  { id: 4, name: '学习编程', icon: '💻', completed: false, streak: 20 },
  { id: 5, name: '冥想 10 分钟', icon: '🧘', completed: false, streak: 3 },
])

// 打卡历史（用于日历和统计）
const checkinHistory = ref({
  '2026-03-14': [1, 2, 3, 4],
  '2026-03-13': [1, 2, 4],
  '2026-03-12': [2, 3, 4, 5],
})

// 当前日期
const currentDate = computed(() => {
  const date = new Date()
  const weekdays = ['周日', '周一', '周二', '周三', '周四', '周五', '周六']
  return {
    day: date.getDate(),
    weekday: weekdays[date.getDay()],
    full: date.toISOString().split('T')[0]
  }
})

// 更新习惯
const updateHabits = (newHabits) => {
  habits.value = newHabits
}
</script>

<style scoped>
.safe-area-bottom {
  padding-bottom: env(safe-area-inset-bottom, 8px);
}
</style>
