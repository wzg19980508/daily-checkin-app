<template>
  <div class="animate-fade-in">
    <h2 class="text-xl font-bold text-gray-800 mb-4">📊 数据统计</h2>
    
    <!-- 总览卡片 -->
    <div class="bg-gradient-to-r from-blue-500 to-purple-600 rounded-2xl p-5 mb-4 text-white card-shadow">
      <div class="text-center">
        <div class="text-4xl font-bold mb-1">{{ totalCheckins }}</div>
        <div class="text-blue-100 text-sm">累计打卡次数</div>
      </div>
    </div>

    <!-- 连续打卡 -->
    <div class="bg-white rounded-2xl p-4 mb-4 card-shadow">
      <h3 class="font-semibold text-gray-800 mb-3">🔥 连续打卡</h3>
      <div class="flex items-center justify-between">
        <div>
          <div class="text-3xl font-bold text-orange-500">{{ maxStreak }}</div>
          <div class="text-sm text-gray-500">最高连续天数</div>
        </div>
        <div class="text-right">
          <div class="text-2xl font-bold text-blue-500">{{ currentStreak }}</div>
          <div class="text-sm text-gray-500">当前连续</div>
        </div>
      </div>
      
      <!-- 火焰动画 -->
      <div class="mt-4 flex justify-center">
        <div class="text-5xl animate-pulse-slow">🔥</div>
      </div>
    </div>

    <!-- 习惯完成率 -->
    <div class="bg-white rounded-2xl p-4 mb-4 card-shadow">
      <h3 class="font-semibold text-gray-800 mb-4">📈 习惯完成率</h3>
      <div class="space-y-3">
        <div v-for="habit in habits" :key="habit.id">
          <div class="flex justify-between items-center mb-1">
            <span class="text-sm text-gray-700">{{ habit.icon }} {{ habit.name }}</span>
            <span class="text-sm font-medium text-gray-600">{{ getHabitCompletion(habit) }}%</span>
          </div>
          <div class="h-2 bg-gray-200 rounded-full overflow-hidden">
            <div 
              class="h-full bg-gradient-to-r from-blue-400 to-purple-500 rounded-full progress-bar"
              :style="{ width: getHabitCompletion(habit) + '%' }"
            ></div>
          </div>
        </div>
      </div>
    </div>

    <!-- 成就徽章 -->
    <div class="bg-white rounded-2xl p-4 card-shadow">
      <h3 class="font-semibold text-gray-800 mb-4">🏆 成就徽章</h3>
      <div class="grid grid-cols-4 gap-3">
        <div 
          v-for="badge in badges" 
          :key="badge.id"
          class="aspect-square rounded-xl flex flex-col items-center justify-center"
          :class="badge.unlocked ? 'bg-gradient-to-br from-yellow-100 to-orange-100' : 'bg-gray-100 opacity-50'"
        >
          <span class="text-2xl">{{ badge.unlocked ? badge.icon : '🔒' }}</span>
          <span class="text-xs text-gray-600 mt-1 text-center">{{ badge.name }}</span>
        </div>
      </div>
    </div>

    <!-- 周统计 -->
    <div class="bg-white rounded-2xl p-4 mt-4 card-shadow">
      <h3 class="font-semibold text-gray-800 mb-4">本周打卡</h3>
      <div class="flex justify-between items-end h-32">
        <div v-for="(count, day) in weekData" :key="day" class="flex flex-col items-center">
          <div 
            class="w-8 bg-gradient-to-t from-blue-400 to-purple-500 rounded-t-lg transition-all hover:from-blue-500 hover:to-purple-600"
            :style="{ height: (count / maxWeekCount * 100) + 'px' }"
          ></div>
          <span class="text-xs text-gray-500 mt-2">{{ day }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  habits: {
    type: Array,
    required: true
  }
})

// 模拟数据
const totalCheckins = 156
const maxStreak = 21
const currentStreak = 7

const getHabitCompletion = (habit) => {
  // 模拟完成率
  const baseRate = 60
  return Math.min(100, baseRate + habit.streak * 2)
}

const badges = [
  { id: 1, name: '初出茅庐', icon: '🌱', unlocked: true },
  { id: 2, name: '持之以恒', icon: '💪', unlocked: true },
  { id: 3, name: '习惯大师', icon: '🎯', unlocked: false },
  { id: 4, name: '完美月度', icon: '👑', unlocked: false },
]

const weekData = {
  '一': 5,
  '二': 4,
  '三': 5,
  '四': 3,
  '五': 5,
  '六': 2,
  '日': 4
}

const maxWeekCount = Math.max(...Object.values(weekData))
</script>
