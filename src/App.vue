<template>
  <PageWidth />
  <div class="bg-gray-200">
    <div
      class="p-4 grid gap-4 md:grid-cols-4 md:grid-rows-2 lg:grid-cols-3 xl:max-w-screen-xl xl:mx-auto"
    >
      <main
        class="bg-gray-50 text-gray-500 shadow-md md:col-span-2 md:row-span-2 lg:col-span-1"
      >
        <div class="relative">
          <img
            class="w-full object-center"
            :src="data.main.imgUrl"
            :alt="data.main.name"
          />
          <h1 class="absolute bottom-0 m-4 text-4xl text-gray-50">
            {{ data.main.name }}
          </h1>
        </div>
        <div class="mt-2 p-4 space-y-6">
          <ul class="space-y-4">
            <li class="flex space-x-4">
              <Briefcase class="w-6 h-6 text-blue-500 stroke-2" />
              <span>{{ data.main.profession }}</span>
            </li>
            <li class="flex space-x-4">
              <HouseIcon />
              <span>{{ data.main.location }}</span>
            </li>
            <li class="flex space-x-4">
              <MailIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <span>{{ data.main.mail }}</span>
            </li>
            <li class="flex space-x-4">
              <!-- TODO: Update icon -->
              <GitHubIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <a :href="data.main.gitHubUrl">{{
                data.main.gitHubUrl.split("/").slice(2).join("/")
              }}</a>
            </li>
            <li class="flex space-x-4">
              <!-- TODO: Update icon -->
              <LinkedinIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <a :href="data.main.linkedInUrl">{{
                data.main.linkedInUrl.split("/").slice(2).join("/")
              }}</a>
            </li>
          </ul>
          <hr />
          <h2 class="flex space-x-4 text-xl font-semibold">
            <SparklesIcon class="w-6 h-6 text-blue-500 stroke-2" />
            <span>Skills</span>
          </h2>
          <ul class="flex flex-wrap">
            <li
              class="bg-blue-600 px-2 mr-1 my-1 rounded-lg text-gray-50 font-semibold"
              v-for="skill in shuffle(data.skills)"
            >
              {{ skill }}
            </li>
          </ul>
          <h2 class="flex space-x-4 text-xl font-semibold">
            <GlobeIcon class="w-6 h-6 text-blue-500 stroke-2" />
            <span>Languages</span>
          </h2>
          <ul class="space-y-4">
            <li class="grid grid-cols-3" v-for="language in data.languages">
              <span>
                {{ language.language }}
              </span>
              <div class="col-span-2 flex justify-between">
                <div
                  class="w-6 h-6 rounded bg-blue-600 border-2 border-blue-700"
                  v-for="n in language.level"
                />
                <div
                  class="w-6 h-6 rounded bg-blue-200 border-2 border-blue-500"
                  v-for="n in 5 - language.level"
                />
              </div>
            </li>
          </ul>
        </div>
      </main>
      <section class="bg-gray-50 shadow-md md:col-span-2">
        <h2>Work Experience</h2>
      </section>
      <section class="bg-gray-50 shadow-md md:col-span-2">
        <h2>Education</h2>
      </section>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent} from "vue";

import Briefcase from "./components/icons/Briefcase.vue";
import HouseIcon from "./components/icons/House.vue";
import MailIcon from "./components/icons/Mail.vue";
import GitHubIcon from "./components/icons/GitHub.vue";
import LinkedinIcon from "./components/icons/Linkedin.vue";
import SparklesIcon from "./components/icons/Sparkles.vue";
import GlobeIcon from "./components/icons/Globe.vue";

import PageWidth from "./components/PageWidth.vue";

import {data} from "./data.ts";

export default defineComponent({
  name: "App",
  components: {
    PageWidth,
    Briefcase,
    HouseIcon,
    MailIcon,
    GitHubIcon,
    LinkedinIcon,
    SparklesIcon,
    GlobeIcon,
  },
  setup() {
    const shuffle = <T>(array: T[]) => {
      // Fisher-Yates algorithm
      for (let i = array.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));

        [array[i], array[j]] = [array[j], array[i]];
      }

      return array;
    };

    return {data, shuffle};
  },
});
</script>
