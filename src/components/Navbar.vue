<template>
  <Disclosure
    as="nav"
    class="fixed top-0 w-full z-50 bg-primary backdrop-blur-md font-roboto h-20 border-b-2 border-secondary"
    v-slot="{ open }"
  >
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8 h-full">
      <div class="relative flex h-full items-center justify-between">
        <!-- Signature on the Left -->
        <div class="flex-shrink-0 flex items-center">
          <img
            class="h-12 w-auto"
            src="../assets/signature.png"
            alt="Signature"
          />
        </div>

        <!-- Desktop Navigation Elements on the Right -->
        <!-- <div class="hidden sm:block">
          <div class="flex space-x-4">
            <a
              v-for="item in navigation"
              :key="item.name"
              :href="item.name === resumeName ? '#' : item.href"
              :class="[
                'relative group rounded-md px-3 py-2 text-md text-black font-medium',
              ]"
              @click="handleClick(item)"
            >
              {{ item.name }}
              <span
                :class="[
                  'absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 -z-10 pointer-events-none blob active-class transition-all duration-300',
                  item.current
                    ? 'opacity-100 scale-100 blob active-class '
                    : 'opacity-0 group-hover:opacity-70 group-hover:scale-90',
                ]"
              ></span>
            </a>
          </div>
        </div> -->
        <div class="hidden sm:block relative">
          <div class="flex space-x-4 relative">
            <span
              class="blob absolute transition-all duration-300"
              :style="{
                top: `${activePosition.top}px`,
                left: `${activePosition.left}px`,
              }"
            ></span>

            <a
              v-for="item in navigation"
              :key="item.name"
              :href="item.name === resumeName ? '#' : item.href"
              class="relative group rounded-md px-3 py-2 text-md text-black font-medium"
              @click="handleClick(item, $event)"
              ref="navItems"
            >
              {{ item.name }}
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
    <!-- <DisclosurePanel class="sm:hidden">
      <div class="space-y-1 px-2 pt-2 pb-3">
        <DisclosureButton
          v-for="item in navigation"
          :key="item.name"
          as="a"
          :href="item.name === resumeName ? '#' : item.href"
          :class="[
            item.current
              ? 'bg-secondary text-black'
              : 'text-black hover:bg-secondary/70',
            'block rounded-md px-3 py-2 text-base font-medium',
          ]"
          :aria-current="item.current ? 'page' : undefined"
          @click="handleClick(item)"
        >
          {{ item.name }}
        </DisclosureButton>
      </div>
    </DisclosurePanel> -->
  </Disclosure>
</template>

<script setup lang="ts">
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";
import { Bars3Icon, XMarkIcon } from "@heroicons/vue/24/solid";
import { reactive } from "vue";
import content from "../assets/content.json";

const resumeName = content.sections.resume;
let navigation = [
  { name: content.sections.about, href: "#landing-page", current: true },
  { name: content.sections.experience, href: "#experience", current: false },
  // { name: content.sections.projects, href: "#", current: false },
  {
    name: content.sections.resume,
    href: content.contact.resumeLink,
    current: false,
  },
  {
    name: content.sections.certifications,
    href: "#certification",
    current: false,
  },
  {
    name: content.sections.contact,
    href: "#contact",
    current: false,
  },
];

// const handleClick = (clickedItem: {
//   name: string;
//   href: string;
//   current: boolean;
// }) => {
//   navigation = navigation.map((navItem) => ({
//     ...navItem,
//     current: navItem.name === clickedItem.name,
//   }));

//   if (clickedItem.name === resumeName) {
//     window.open(clickedItem.href, "_blank");
//   }
// };

const activePosition = reactive({ top: 0, left: 0 });

const handleClick = (
  item: {
    name: string;
    href: string;
    current: boolean;
  },
  event: MouseEvent
) => {
  navigation = navigation.map((navItem) => ({
    ...navItem,
    current: navItem.name === item.name,
  }));

  const target = event.currentTarget as HTMLElement | null;
  if (target) {
    activePosition.top = target.offsetTop;
    activePosition.left = target.offsetLeft;
  }

  if (item.name === resumeName) {
    window.open(item.href, "_blank");
  }
};
</script>

<style scoped>
.blob {
  position: absolute;
  width: 60px;
  height: 40px;
  background-color: #0fa3b1;
  border-radius: 94% 31% 30% 67% / 67% 37% 56% 34%;
  transition: all 0.3s ease-in-out;
}

.active-class {
  opacity: 1;
  transform: scale(1);
}

.group:hover .blob {
  opacity: 0.7;
  transform: scale(0.9);
}
</style>
