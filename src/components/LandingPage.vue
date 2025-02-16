<template>
  <div
    class="container mx-auto flex flex-col md:flex-row items-center justify-between p-16 font-raleway"
  >
    <div class="md:w-3/4 mb-6 md:pr-20 md:mb-0">
      <div class="text-[60px] mb-4">{{ title }} {{ displayRoles }}</div>
      <p class="text-lg leading-relaxed">
        {{ description }}
      </p>
    </div>
    <div class="md:w-1/4 flex justify-center relative">
      <img
        src="../assets/profile.png"
        alt="Anushree Image"
        class="w-[400px] h-[350px] object-cover rounded-[80px] relative z-10"
      />
      <span
        :class="'absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 pointer-events-none blob'"
      ></span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import content from "../../public/content.json";

const title = ref(content.title);
const description = ref(content.description["landing-page"]);
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

<style scoped>
.blob {
  border-radius: 94% 31% 30% 67% / 67% 37% 56% 34%;
  width: 300px;
  height: 350px;
  background-color: #0fa3b1;
  opacity: 0.85;
  box-shadow: -10vmin 10vmin 0 rgba(255, 255, 255, 0.07);
  z-index: 0;
  transform: rotate(140deg);
}
</style>
