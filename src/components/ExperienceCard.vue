<template>
  <div class="w-full mt-4 font-raleway">
    <div class="w-full rounded-2xl bg-white p-2">
      <Disclosure as="div" v-slot="{ open }">
        <DisclosureButton
          class="flex flex-row items-center w-full justify-between rounded-lg bg-white px-4 py-2 text-left hover:bg-secondary/40 focus:outline-none focus-visible:ring focus-visible:ring-secondary/75"
        >
          <div class="flex flex-row justify-start items-baseline">
            <span class="text-heading text-black">{{ content.title }}</span>
            <span class="pl-2 text-regular text-black">{{
              content.location
            }}</span>
          </div>
          <ChevronUpIcon
            :class="open ? 'rotate-180 transform' : ''"
            class="h-8 w-8 text-secondary"
          />
        </DisclosureButton>
        <DisclosurePanel class="px-4 pb-2 pt-4 text-small text-black/80">
          <p class="text-small font-bold">{{ content.timeline }}</p>
          <ul class="list-disc list-inside mt-2">
            <li
              v-for="(point, index) in content.description"
              :key="index"
              class="text-small"
            >
              {{ point }}
            </li>
          </ul>
        </DisclosurePanel>
      </Disclosure>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";
import { ChevronUpIcon } from "@heroicons/vue/20/solid";

interface Experience {
  title: string;
  location: string;
  timeline: string;
  description: string[];
}

interface Props {
  content: Experience;
}

defineProps<Props>();
</script>
