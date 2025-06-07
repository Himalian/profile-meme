<script setup>
import { onMounted, ref, watch } from 'vue';

const STORAGE_KEY = 'characters';
// 定义四个格子的初始数据
const characters = ref([
  { name: '', description: '', avatar: '/src/assets/default-profile.png' },
  { name: '', description: '', avatar: '/src/assets/default-profile.png' },
  { name: '', description: '', avatar: '/src/assets/default-profile.png' },
  { name: '', description: '', avatar: '/src/assets/default-profile.png' }
]);

onMounted(()=>{
	const saved = localStorage.getItem(STORAGE_KEY);

	if (saved) {
		characters.value = JSON.parse(saved)
	}
})

watch(characters, (newVal) => {
	localStorage.setItem(STORAGE_KEY, JSON.stringify(newVal.filter(item => item.name || item.description)))
}, { deep: true })
</script>

<template>
  <div class="grid grid-cols-2 grid-rows-2 gap-4 w-fit p-4">
    <div 
      v-for="(item, index) in characters" 
      :key="index"
      class="flex flex-col items-center justify-center"
    >
      <!-- 头像部分 -->
      <img 
        :src="item.avatar" 
        class="w-24 h-24 mb-2 border-black border rounded-full object-cover"
      >
      <!-- 输入部分：双向绑定到数组项 -->
      <input 
        v-model="item.name"
        placeholder=""
        class="font-bold text-2xl w-full text-center border-none focus:border-b focus:border-black"
      >
	  <input 
		v-model="item.description"
		placeholder=""
		class="w-full text-center border-none focus:border-b focus:border-black"
	  >
    </div>
  </div>
</template>