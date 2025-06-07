<script setup lang="ts">
import { useLocalStorage } from '@vueuse/core';
import mobile from 'is-mobile';
import mixpanel from 'mixpanel-browser';
import { provide, ref, toRaw } from 'vue';
import bg from '@/assets/bg.jpg';
import PartHighlight from '@/components/part/Highlight.vue';
import PartNotes from '@/components/part/Notes.vue';
import PartProspect from '@/components/Prospect.vue';
import PartRating from '@/components/part/Rating.vue';
import SubmitterInput from '@/components/SubmitterInput.vue';
import { Button } from '@/components/ui/button';
import { Checkbox } from '@/components/ui/checkbox';
import { Dialog, DialogContent, DialogDescription, DialogFooter, DialogHeader, DialogTitle } from '@/components/ui/dialog';
import { Label } from '@/components/ui/label';
import { Separator } from '@/components/ui/separator';
import { FormInjectKey, getDefaultForm } from '@/utils/form';

if (!import.meta.env.DEV) {
  mixpanel.init(import.meta.env.MAI_MIXPANEL_TOKEN, {
    track_pageview: true,
  });
}

const form = useLocalStorage('form', getDefaultForm());
provide(FormInjectKey, form);

const saving = ref(false);
const sendAnonymousData = ref(true);

async function confirm() {
  saving.value = false;
  if (sendAnonymousData.value) {
    mixpanel.track('Save Report', {
      Form: {
        ...toRaw(form.value),
        submitter: undefined, // 匿名处理
      },
    });
  }
}
</script>

<template>
  <div class="flex items-center w-120 mx-auto mb-2">
    <p class="mr-2">
      点击报告各部分即可填写～(∠・ω&lt; )⌒☆
    </p>
    <Button @click="saving = true">
      保存为图片
    </Button>
  </div>

  <div
    class="w-120 h-165 mx-auto border border-black rounded-lg gap-4 flex flex-col"
    :style="{
    }"
  >
    <div class="flex justify-between">
      <div class="flex items-center">
        <h1 class="text-2xl font-bold">
			登场人物介绍
        </h1>
      </div>
    </div>

      <PartProspect />
  </div>

</template>
