<template>
  <div class="container mx-auto p-16 font-roboto">
    <div class="flex flex-row justify-items-start items-center gap-4 mb-6">
      <svg
        class="w-[50px] h-[50px] fill-secondary"
        viewBox="0 0 512 512"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M370.7 96.1C346.1 39.5 289.7 0 224 0S101.9 39.5 77.3 96.1C60.9 97.5 48 111.2 48 128v64c0 16.8 12.9 30.5 29.3 31.9C101.9 280.5 158.3 320 224 320s122.1-39.5 146.7-96.1c16.4-1.4 29.3-15.1 29.3-31.9V128c0-16.8-12.9-30.5-29.3-31.9zM336 144v16c0 53-43 96-96 96H208c-53 0-96-43-96-96V144c0-26.5 21.5-48 48-48H288c26.5 0 48 21.5 48 48zM189.3 162.7l-6-21.2c-.9-3.3-3.9-5.5-7.3-5.5s-6.4 2.2-7.3 5.5l-6 21.2-21.2 6c-3.3 .9-5.5 3.9-5.5 7.3s2.2 6.4 5.5 7.3l21.2 6 6 21.2c.9 3.3 3.9 5.5 7.3 5.5s6.4-2.2 7.3-5.5l6-21.2 21.2-6c3.3-.9 5.5-3.9 5.5-7.3s-2.2-6.4-5.5-7.3l-21.2-6zM112.7 316.5C46.7 342.6 0 407 0 482.3C0 498.7 13.3 512 29.7 512H128V448c0-17.7 14.3-32 32-32H288c17.7 0 32 14.3 32 32v64l98.3 0c16.4 0 29.7-13.3 29.7-29.7c0-75.3-46.7-139.7-112.7-165.8C303.9 338.8 265.5 352 224 352s-79.9-13.2-111.3-35.5zM176 448c-8.8 0-16 7.2-16 16v48h32V464c0-8.8-7.2-16-16-16zm96 32a16 16 0 1 0 0-32 16 16 0 1 0 0 32z"
        ></path>
      </svg>

      <h1 class="text-huge">
        {{ pageTitle }}
      </h1>
    </div>

    <div class="flex flex-cols">
      <div
        class="border-l-2 pl-6 ml-6 border-dashed bl-3 border-tertiary h-full"
      >
        <h2 class="text-black text-heading mt-10">{{ description }}</h2>

        <h2 class="mt-10 text-black text-heading font-semibold">
          Email : {{ email }}
        </h2>
        <div
          class="flex flex-row text-black mt-10 mb-10 text-regular items-center gap-10"
        >
          <button @click="openLink('linkedin')" class="cursor-pointer">
            <svg
              class="w-[50px] h-[50px] fill-secondary"
              viewBox="0 0 512 512"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M100.28 448H7.4V148.9h92.88zM53.79 108.1C24.09 108.1 0 83.5 0 53.8a53.79 53.79 0 0 1 107.58 0c0 29.7-24.1 54.3-53.79 54.3zM447.9 448h-92.68V302.4c0-34.7-.7-79.2-48.29-79.2-48.29 0-55.69 37.7-55.69 76.7V448h-92.78V148.9h89.08v40.8h1.3c12.4-23.5 42.69-48.3 87.88-48.3 94 0 111.28 61.9 111.28 142.3V448z"
              ></path>
            </svg>
          </button>
          <button
            @click="openLink('resume')"
            class="bg-secondary hover:bg-secondary/70 cursor-pointer text-white font-semibold py-2 px-4 rounded transition-colors duration-300"
          >
            {{ resume }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import content from "../assets/content.json";

const pageTitle = content.sections.contact;
const resume = content.sections.resume;
const description = content.contact.description;
const email = content.contact.email;
const linkedinLink = content.contact.linkedinLink;
const resumeLink = content.contact.resumeLink;

const openLink = (value: string) => {
  if (value === "resume") {
    window.open(resumeLink, "_blank");
  } else {
    window.open(linkedinLink, "_blank");
  }
};
</script>

<style scoped></style>
