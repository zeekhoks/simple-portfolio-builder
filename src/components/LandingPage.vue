<template>
  <div
    class="container mx-auto flex flex-col md:flex-row items-center justify-between p-16 font-roboto"
  >
    <div class="md:w-1/2 mb-6 md:pr-20 md:mb-0">
      <h1 class="text-huge mb-4">
        {{ title }}
      </h1>
      <h1 class="text-medium mb-4">A {{ displayRoles }}</h1>
      <p class="text-regular leading-relaxed">
        {{ description }}
      </p>
    </div>
    <div class="md:w-1/2 flex justify-center relative">
      <img
        src="../assets/anushreeprofile.png"
        alt="Anushree Image"
        class="w-[400px] h-[400px] object-contain"
      />
      <!-- <span
        :class="'absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 pointer-events-none blob'"
      ></span> -->
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import content from "../assets/content.json";

const title = content.title;
const description = content.description["landing-page"];
// const description_second = content.description["landing-page-second"];
const displayRoles = ref("");
const charIndex = ref(0);
const roleIndex = ref(0);
const roles = ref([
  content.roles["data-analyst"],
  content.roles["data-engineer"],
  content.roles["cloud-enthusiast"],
]);

const typingSpeed = 150;
const deletingSpeed = 150;
const pauseBeforeDelete = 1000;
const pausedBeforeNextRole = 500;

const typingEffect = () => {
  const currentRole = roles.value[roleIndex.value];
  let typingIntervalId = setInterval(() => {
    if (charIndex.value < currentRole.length) {
      displayRoles.value += currentRole[charIndex.value];
      charIndex.value += 1;
    } else {
      clearInterval(typingIntervalId);
      setTimeout(() => {
        deletingEffect();
      }, pauseBeforeDelete);
    }
  }, typingSpeed);
};

const deletingEffect = () => {
  let deletingIntervalId = setInterval(() => {
    if (displayRoles.value.length > 0) {
      displayRoles.value = displayRoles.value.slice(0, -1);
    } else {
      clearInterval(deletingIntervalId);
      charIndex.value = 0;
      roleIndex.value = (roleIndex.value + 1) % roles.value.length;
      setTimeout(() => {
        typingEffect();
      }, pausedBeforeNextRole);
    }
  }, deletingSpeed);
};

onMounted(() => {
  typingEffect();
});
</script>

<style scoped></style>
