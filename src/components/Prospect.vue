<script setup>
import { onMounted, ref, watch } from 'vue';
import Avatar from './Avatar.vue';

const STORAGE_KEY = 'characters';
// 定义四个格子的初始数据
const defaultAvatar = '@assets/default-profile.png';
const characters = ref([
	{ name: '', description: '', avatar: defaultAvatar },
	{ name: '', description: '', avatar: defaultAvatar },
	{ name: '', description: '', avatar: defaultAvatar },
	{ name: '', description: '', avatar: defaultAvatar }
]);

onMounted(() => {
	const saved = localStorage.getItem(STORAGE_KEY);

	if (saved) {
		characters.value = JSON.parse(saved)
	}
})

watch(characters, (newVal) => {
	localStorage.setItem(STORAGE_KEY, JSON.stringify(newVal))
}, { deep: true })
</script>

<template>
	<div class="grid grid-cols-2 grid-rows-2 gap-4 w-fit p-4">
		<div v-for="(item, index) in characters" :key="index" class="flex flex-col items-center justify-center">
			<!-- 头像部分 -->
			<Avatar :src="item.avatar" @update:src="(val) => item.avatar = val" />
			<!-- 输入部分：双向绑定到数组项 -->
			<input v-model="item.name" placeholder=""
				class="font-bold text-2xl w-full text-center border border-transparent focus:outline-none focus:border-b focus:border-black hover:border-zinc-600 break-all transition-colors">

			<input v-model="item.description" placeholder=""
				class="max-w-full text-center border border-transparent focus:outline-none focus:border-b focus:border-black hover:border-zinc-600 break-all transition-colors">
		</div>
	</div>
</template>