<script setup lang="ts">
	
import { useLocalStorage } from '@vueuse/core';
import mobile from 'is-mobile';
import mixpanel from 'mixpanel-browser';
import { provide, ref, toRaw } from 'vue';
import Prospect from './components/Prospect.vue';
import download from 'downloadjs';
import { domToPng } from 'modern-screenshot';


async function handleSaveToImageClick() {
	const node = document.getElementById('meme-container')
	domToPng(node as HTMLElement, {quality: 1, scale: 2}).then((dataUrl) => {download(dataUrl, 'meme.png')})
	
}

</script>

<template>
  <div class="flex justify-between items-center mt-2 mx-auto mb-2 w-auto">
    <p class="mr-2">
      点击报告各部分即可填写～(∠・ω&lt; )⌒☆
    </p>
    <Button 
	class='rounded-xl p-1.5  border-transparent bg-zinc-800 text-white hover:bg-zinc-600 hover:cursor-pointer hover:border-black transition-colors'
	@click="handleSaveToImageClick">
      保存为图片
    </Button>
  </div>

  <div
  	id="meme-container"
    class="w-auto min-h-165 h-auto mx-auto border bg-white border-black rounded-lg gap-4 flex flex-col"
    :style="{
    }"
  >
    <div class="flex justify-between">
      <div class="flex items-center">
        <h1 class="text-2xl font-bold mt-2 ml-2">
			登场人物介绍
        </h1>
      </div>
    </div>

      <Prospect />
  </div>

</template>
