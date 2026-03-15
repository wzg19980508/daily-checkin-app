<template>
  <div class="animate-fade-in">
    <h2 class="text-xl font-bold text-gray-800 mb-4">📆 打卡日历</h2>
    
    <!-- 月份选择 -->
    <div class="bg-white rounded-2xl p-4 mb-4 card-shadow">
      <div class="flex justify-between items-center mb-4">
        <button @click="previousMonth" class="p-2 hover:bg-gray-100 rounded-lg transition-colors">
          <span class="text-xl">◀</span>
        </button>
        <span class="text-lg font-semibold">{{ currentMonthYear }}</span>
        <button @click="nextMonth" class="p-2 hover:bg-gray-100 rounded-lg transition-colors">
          <span class="text-xl">▶</span>
        </button>
      </div>
      
      <!-- 星期标题 -->
      <div class="grid grid-cols-7 gap-1 mb-2">
        <div v-for="day in ['日', '一', '二', '三', '四', '五', '六']" :key="day" 
             class="text-center text-sm text-gray-500 py-2">
          {{ day }}
        </div>
      </div>
      
      <!-- 日历网格 -->
      <div class="grid grid-cols-7 gap-1">
        <!-- 空白填充 -->
        <div v-for="i in firstDayOfMonth" :key="'empty-' + i" class="aspect-square"></div>
        
        <!-- 日期格子 -->
        <div 
          v-for="day in daysInMonth" 
          :key="day"
          class="aspect-square calendar-day rounded-lg flex items-center justify-center text-sm font-medium relative"
          :class="getDayClass(day)"
        >
          {{ day }}
          <span v-if="isToday(day)" class="absolute -top-1 -right-1 w-3 h-3 bg-red-500 rounded-full"></span>
        </div>
      </div>
    </div>

    <!-- 图例 -->
    <div class="bg-white rounded-2xl p-4 card-shadow">
      <h3 class="font-semibold text-gray-800 mb-3">图例说明</h3>
      <div class="flex flex-wrap gap-3">
        <div class="flex items-center space-x-2">
          <div class="w-6 h-6 bg-gradient-to-r from-green-400 to-green-500 rounded"></div>
          <span class="text-sm text-gray-600">全勤</span>
        </div>
        <div class="flex items-center space-x-2">
          <div class="w-6 h-6 bg-blue-100 rounded"></div>
          <span class="text-sm text-gray-600">部分完成</span>
        </div>
        <div class="flex items-center space-x-2">
          <div class="w-6 h-6 bg-red-100 rounded"></div>
          <span class="text-sm text-gray-600">未完成</span>
        </div>
        <div class="flex items-center space-x-2">
          <div class="w-6 h-6 bg-gray-100 rounded border-2 border-red-500"></div>
          <span class="text-sm text-gray-600">今天</span>
        </div>
      </div>
    </div>

    <!-- 本月统计 -->
    <div class="bg-white rounded-2xl p-4 mt-4 card-shadow">
      <h3 class="font-semibold text-gray-800 mb-3">本月统计</h3>
      <div class="grid grid-cols-2 gap-4">
        <div class="text-center">
          <div class="text-2xl font-bold text-green-500">{{ perfectDays }}</div>
          <div class="text-xs text-gray-500">全勤天数</div>
        </div>
        <div class="text-center">
          <div class="text-2xl font-bold text-blue-500">{{ completionRate }}%</div>
          <div class="text-xs text-gray-500">完成率</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const currentDate = ref(new Date())

const currentMonthYear = computed(() => {
  const year = currentDate.value.getFullYear()
  const month = currentDate.value.getMonth() + 1
  return `${year}年${month}月`
})

const daysInMonth = computed(() => {
  const year = currentDate.value.getFullYear()
  const month = currentDate.value.getMonth()
  return new Date(year, month + 1, 0).getDate()
})

const firstDayOfMonth = computed(() => {
  const year = currentDate.value.getFullYear()
  const month = currentDate.value.getMonth()
  return new Date(year, month, 1).getDay()
})

const today = new Date()

const isToday = (day) => {
  return day === today.getDate() && 
         currentDate.value.getMonth() === today.getMonth() && 
         currentDate.value.getFullYear() === today.getFullYear()
}

const getDayClass = (day) => {
  const dateKey = `${currentDate.value.getFullYear()}-${String(currentDate.value.getMonth() + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`
  
  if (isToday(day)) {
    return 'bg-gray-100 border-2 border-red-500 text-gray-800'
  }
  
  // 模拟数据：根据日期奇偶性判断完成状态
  if (day % 3 === 0) {
    return 'bg-gradient-to-r from-green-400 to-green-500 text-white'
  } else if (day % 2 === 0) {
    return 'bg-blue-100 text-blue-800'
  } else {
    return 'bg-red-100 text-red-800'
  }
}

const perfectDays = computed(() => {
  // 模拟数据
  return Math.floor(daysInMonth.value / 3)
})

const completionRate = computed(() => {
  // 模拟数据
  return Math.round((perfectDays.value / daysInMonth.value) * 100)
})

const previousMonth = () => {
  currentDate.value = new Date(currentDate.value.getFullYear(), currentDate.value.getMonth() - 1, 1)
}

const nextMonth = () => {
  currentDate.value = new Date(currentDate.value.getFullYear(), currentDate.value.getMonth() + 1, 1)
}
</script>
