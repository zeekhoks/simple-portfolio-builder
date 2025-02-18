<template>
  <div
    class="w-full mt-4 font-raleway rounded-[20px] border p-4 bg-white border-secondary"
  >
    <div class="flex justify-center">
      <img
        class="h-50 w-50 overflow-hidden rounded-full"
        :src="getImageUrl(content.filename)"
        alt="Logo"
      />
    </div>
    <div class="mt-4 text-left">
      <p class="text-black text-regular font-bold">{{ content.title }}</p>
      <p class="text-black text-small">{{ content.issued }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Certification {
  filename: string;
  title: string;
  issued: string;
}

interface Props {
  content: Certification;
}

const props = defineProps<Props>();
function getImageUrl(name: string) {
  return new URL(`../assets/${name}.png`, import.meta.url).href;
}
</script>
