<template>
  <div class="animate-fade-in">
    <!-- 进度概览 -->
    <div class="bg-white rounded-2xl p-4 mb-4 card-shadow">
      <div class="flex justify-between items-center mb-3">
        <h2 class="text-lg font-semibold text-gray-800">今日进度</h2>
        <span class="text-sm text-gray-500">{{ completedCount }}/{{ habits.length }}</span>
      </div>
      
      <!-- 进度条 -->
      <div class="h-3 bg-gray-200 rounded-full overflow-hidden">
        <div 
          class="h-full bg-gradient-to-r from-blue-500 to-purple-500 progress-bar rounded-full"
          :style="{ width: progressPercent + '%' }"
        ></div>
      </div>
      
      <!-- 鼓励语 -->
      <p v-if="progressPercent === 100" class="text-center text-green-600 font-medium mt-2">
        🎉 太棒了！今日任务全部完成！
      </p>
      <p v-else-if="progressPercent > 0" class="text-center text-blue-600 font-medium mt-2">
        💪 继续加油！已经完成{{ progressPercent }}%
      </p>
      <p v-else class="text-center text-gray-500 font-medium mt-2">
        🌟 开始今天的打卡吧！
      </p>
    </div>

    <!-- 习惯列表 -->
    <div class="space-y-3">
      <div 
        v-for="habit in habits" 
        :key="habit.id"
        class="bg-white rounded-2xl p-4 card-shadow animate-fade-in flex items-center justify-between"
        :class="{ 'opacity-75': habit.completed }"
      >
        <div class="flex items-center space-x-3">
          <span class="text-3xl">{{ habit.icon }}</span>
          <div>
            <h3 class="font-medium text-gray-800">{{ habit.name }}</h3>
            <p class="text-xs text-orange-500">🔥 连续{{ habit.streak }}天</p>
          </div>
        </div>
        
        <button
          @click="toggleCheckin(habit)"
          class="checkin-btn w-14 h-14 rounded-full flex items-center justify-center transition-all transform active:scale-95"
          :class="habit.completed 
            ? 'bg-gradient-to-r from-green-400 to-green-500 text-white shadow-lg shadow-green-300' 
            : 'bg-gradient-to-r from-blue-400 to-blue-500 text-white shadow-lg shadow-blue-300'"
        >
          <span v-if="habit.completed" class="text-2xl animate-checkmark">✓</span>
          <span v-else class="text-2xl">+</span>
        </button>
      </div>
    </div>

    <!-- 添加新习惯按钮 -->
    <button 
      @click="showAddModal = true"
      class="fixed bottom-20 right-6 w-14 h-14 bg-gradient-to-r from-purple-500 to-pink-500 text-white rounded-full shadow-lg flex items-center justify-center text-3xl hover:scale-110 transition-transform"
    >
      +
    </button>

    <!-- 添加习惯弹窗 -->
    <div v-if="showAddModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50 p-4" @click.self="showAddModal = false">
      <div class="bg-white rounded-2xl p-6 w-full max-w-sm animate-fade-in">
        <h3 class="text-xl font-bold text-gray-800 mb-4">添加新习惯</h3>
        
        <input 
          v-model="newHabitName"
          type="text" 
          placeholder="输入习惯名称..."
          class="w-full border border-gray-300 rounded-xl px-4 py-3 mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
          @keyup.enter="addHabit"
        />
        
        <div class="flex space-x-2 mb-4">
          <button 
            v-for="icon in ['🏃', '📚', '🥗', '💻', '🧘', '💤', '🎯', '✍️']" 
            :key="icon"
            @click="selectedIcon = icon"
            :class="['text-2xl p-2 rounded-lg transition-all', selectedIcon === icon ? 'bg-blue-100 ring-2 ring-blue-500' : 'bg-gray-100']"
          >
            {{ icon }}
          </button>
        </div>
        
        <div class="flex space-x-3">
          <button 
            @click="showAddModal = false"
            class="flex-1 py-3 bg-gray-100 text-gray-700 rounded-xl font-medium"
          >
            取消
          </button>
          <button 
            @click="addHabit"
            class="flex-1 py-3 bg-gradient-to-r from-blue-500 to-purple-500 text-white rounded-xl font-medium"
          >
            添加
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const props = defineProps({
  habits: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['update:habits'])

const showAddModal = ref(false)
const newHabitName = ref('')
const selectedIcon = ref('🎯')

const completedCount = computed(() => {
  return props.habits.filter(h => h.completed).length
})

const progressPercent = computed(() => {
  if (props.habits.length === 0) return 0
  return Math.round((completedCount.value / props.habits.length) * 100)
})

const toggleCheckin = (habit) => {
  const updated = props.habits.map(h => {
    if (h.id === habit.id) {
      return { ...h, completed: !h.completed }
    }
    return h
  })
  emit('update:habits', updated)
}

const addHabit = () => {
  if (!newHabitName.value.trim()) return
  
  const newHabit = {
    id: Date.now(),
    name: newHabitName.value.trim(),
    icon: selectedIcon.value,
    completed: false,
    streak: 0
  }
  
  emit('update:habits', [...props.habits, newHabit])
  newHabitName.value = ''
  showAddModal.value = false
}
</script>
