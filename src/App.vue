<template>
  <!-- <PageWidth /> -->
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

        <div class="mt-2 p-4 space-y-8">
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
          <div>
            <h3 class="flex space-x-4 text-xl font-semibold">
              <SparklesIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <span>Skills</span>
            </h3>
            <ul class="mt-4 flex flex-wrap">
              <li
                class="bg-blue-600 px-2 mr-1 my-1 rounded-lg text-gray-50 font-semibold"
                v-for="skill in shuffle(data.skills)"
              >
                {{ skill }}
              </li>
            </ul>
          </div>
          <div>
            <h3 class="flex space-x-4 text-xl font-semibold">
              <GlobeIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <span>Languages</span>
            </h3>
            <ul class="mt-4 space-y-4">
              <li class="grid grid-cols-3" v-for="language in data.languages">
                <span>
                  {{ language.language }}
                </span>
                <div class="col-span-2 flex justify-between">
                  <div
                    class="w-8 h-6 rounded bg-blue-600 border-2 border-blue-700 hover:animate-wiggle"
                    v-for="n in language.level"
                  />
                  <div
                    class="w-8 h-6 rounded bg-blue-200 border-2 border-blue-500 hover:animate-wiggle"
                    v-for="n in 5 - language.level"
                  />
                </div>
              </li>
            </ul>
          </div>
        </div>
      </main>

      <section class="p-4 space-y-6 bg-gray-50 shadow-md md:col-span-2">
        <h2 class="flex space-x-4 text-2xl font-semibold text-gray-500">
          <CodeIcon class="w-8 h-8 text-blue-500 stroke-2" />
          <span>Work Experience</span>
        </h2>
        <ul class="divide-y">
          <li class="py-4" v-for="work in data.workExperience">
            <h3 class="text-xl font-semibold text-gray-500">{{ work.role }}</h3>
            <a class="text-lg text-blue-700" :href="work.homepage">{{
              work.company
            }}</a>
            <div class="flex items-center">
              <CalendarIcon class="w-5 h-5 text-blue-500 stroke-2" />
              <span class="ml-2 text-blue-500"
                >{{
                  work.start.toLocaleDateString("en-GB", {
                    year: "numeric",
                    month: "long",
                  })
                }}
                -
                {{
                  work.end
                    ? work.end.toLocaleDateString("en-GB", {
                        year: "numeric",
                        month: "long",
                      })
                    : "Present"
                }}</span
              >
            </div>
            <p class="mt-2 text-gray-800">{{ work.description }}</p>
          </li>
        </ul>
      </section>

      <section class="p-4 space-y-6 bg-gray-50 shadow-md md:col-span-2">
        <h2 class="flex space-x-4 text-2xl font-semibold text-gray-500">
          <AcademicCapIcon class="w-8 h-8 text-blue-500 stroke-2" />
          <span>Education</span>
        </h2>
        <ul class="divide-y">
          <li class="py-4" v-for="stop in data.education">
            <h3 class="text-xl font-semibold text-gray-500">
              {{ stop.degree }}
            </h3>
            <a class="text-lg text-blue-700" :href="stop.homepage">{{
              stop.location
            }}</a>
            <div class="flex items-center">
              <CalendarIcon class="w-5 h-5 text-blue-500 stroke-2" />
              <span class="ml-2 text-blue-500"
                >{{
                  stop.start.toLocaleDateString("en-GB", {
                    year: "numeric",
                    month: "long",
                  })
                }}
                -
                {{
                  stop.end
                    ? stop.end.toLocaleDateString("en-GB", {
                        year: "numeric",
                        month: "long",
                      })
                    : "Stopped"
                }}</span
              >
            </div>
            <p class="mt-2 text-gray-800">{{ stop.description }}</p>
          </li>
        </ul>
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
import PresentationChartIcon from "./components/icons/PresentationChart.vue";
import CodeIcon from "./components/icons/Code.vue";
import CalendarIcon from "./components/icons/Calendar.vue";
import AcademicCapIcon from "./components/icons/AcademicCap.vue";

import PageWidth from "./components/PageWidth.vue";
import ProjectCard from "./components/ProjectCard.vue";

import {data} from "./data.ts";

export default defineComponent({
  name: "App",
  components: {
    PageWidth,
    ProjectCard,
    Briefcase,
    HouseIcon,
    MailIcon,
    GitHubIcon,
    LinkedinIcon,
    SparklesIcon,
    GlobeIcon,
    PresentationChartIcon,
    CodeIcon,
    CalendarIcon,
    AcademicCapIcon,
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
