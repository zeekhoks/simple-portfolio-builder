<template>
  <Disclosure
    as="nav"
    class="fixed top-0 w-full z-50 bg-primary backdrop-blur-md font-raleway h-20 border-b-2 border-secondary"
    v-slot="{ open }"
  >
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8 h-full">
      <div class="relative flex h-full items-center justify-between">
        <!-- Signature on the Left -->
        <div class="flex-shrink-0 flex items-center">
          <img
            class="h-12 w-auto"
            src="../assets/singature.png"
            alt="Signature"
          />
        </div>

        <!-- Desktop Navigation Elements on the Right -->
        <div class="hidden sm:block">
          <div class="flex space-x-4">
            <a
              v-for="item in navigation"
              :key="item.name"
              :href="item.href"
              :class="[
                'relative group rounded-md px-3 py-2 text-md text-black font-medium',
              ]"
              :aria-current="item.current ? 'page' : undefined"
            >
              {{ item.name }}
              <span
                :class="[
                  'absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 -z-10 pointer-events-none blob transition-all duration-300',
                  item.current
                    ? 'opacity-100 scale-100'
                    : 'opacity-0 group-hover:opacity-70 group-hover:scale-90',
                ]"
              ></span>
            </a>
          </div>
        </div>

        <!-- Mobile Menu Button on the Right -->
        <div class="absolute inset-y-0 right-0 flex items-center sm:hidden">
          <DisclosureButton
            class="relative inline-flex items-center justify-center rounded-md p-2 text-black hover:bg-secondary"
          >
            <span class="sr-only">Open main menu</span>
            <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
            <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
          </DisclosureButton>
        </div>
      </div>
    </div>

    <!-- Mobile Menu -->
    <DisclosurePanel class="sm:hidden">
      <div class="space-y-1 px-2 pt-2 pb-3">
        <DisclosureButton
          v-for="item in navigation"
          :key="item.name"
          as="a"
          :href="item.href"
          :class="[
            item.current
              ? 'bg-secondary text-black'
              : 'text-black hover:bg-secondary/70',
            'block rounded-md px-3 py-2 text-base font-medium',
          ]"
          :aria-current="item.current ? 'page' : undefined"
        >
          {{ item.name }}
        </DisclosureButton>
      </div>
    </DisclosurePanel>
  </Disclosure>
</template>

<script setup lang="ts">
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";
import { Bars3Icon, XMarkIcon } from "@heroicons/vue/24/solid";
import content from "../../public/content.json";

const navigation = [
  { name: content.btn.about, href: "#", current: true },
  { name: content.btn.experience, href: "#", current: false },
  { name: content.btn.projects, href: "#", current: false },
  { name: content.btn.certifications, href: "#", current: false },
];
</script>

<style scoped>
.blob {
  border-radius: 94% 31% 30% 67% / 67% 37% 56% 34%;
  width: 60px;
  height: 40px;
  background-color: #0fa3b1;
  box-shadow: -10vmin 10vmin 0 rgba(255, 255, 255, 0.07);
}
</style>
