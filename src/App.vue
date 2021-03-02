<template>
  <!-- <PageWidth /> -->
  <div class="bg-gray-200">
    <div
      class="p-4 grid gap-4 md:grid-cols-4 md:grid-rows-3 lg:grid-cols-3 xl:max-w-screen-xl xl:mx-auto"
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
          <h1 class="absolute bottom-0 m-4 text-4xl text-white">
            {{ data.main.name }}
          </h1>
        </div>

        <div class="mt-2 p-4 space-y-8">
          <ul class="space-y-4">
            <li class="flex items-center space-x-4">
              <Briefcase class="w-6 h-6 text-blue-500 stroke-2" />
              <span>{{ data.main.profession }}</span>
            </li>
            <li class="flex items-center space-x-4">
              <HouseIcon />
              <span>{{ data.main.location }}</span>
            </li>
            <li class="flex items-center space-x-4">
              <MailIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <span>{{ data.main.mail }}</span>
            </li>
            <li class="flex items-center space-x-4">
              <!-- TODO: Update icon -->
              <GitHubIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <a :href="data.main.gitHubUrl" target="_blank">{{
                data.main.gitHubUrl.split("/").slice(2).join("/")
              }}</a>
            </li>
            <li class="flex items-center space-x-4">
              <!-- TODO: Update icon -->
              <LinkedinIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <a :href="data.main.linkedInUrl" target="_blank">{{
                data.main.linkedInUrl.split("/").slice(2).join("/")
              }}</a>
            </li>
          </ul>
          <hr />
          <div>
            <h3 class="flex items-center space-x-4 text-xl font-semibold">
              <SparklesIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <span>Skills</span>
            </h3>
            <ul class="mt-4 flex flex-wrap">
              <li
                class="border border-blue-600 px-2 mr-1 my-1 rounded-lg text-blue-600 font-semibold cursor-default hover:bg-blue-600 hover:text-white"
                v-for="skill in shuffle(data.skills)"
                :key="skill"
              >
                {{ skill }}
              </li>
            </ul>
          </div>
          <div>
            <h3 class="flex items-center space-x-4 text-xl font-semibold">
              <FlagIcon class="w-6 h-6 text-blue-500 stroke-2" />
              <span>Languages</span>
            </h3>
            <ul class="mt-4 space-y-4">
              <li
                class="grid grid-cols-3"
                v-for="language in data.languages"
                :key="language"
              >
                <span>
                  {{ language.language }}
                </span>
                <div class="col-span-2 flex justify-between">
                  <FlagIcon
                    class="w-6 h-6 text-blue-600 stroke-2 fill-current"
                    v-for="n in language.level"
                    :key="n"
                  />
                  <FlagIcon
                    class="w-6 h-6 text-blue-500 stroke-2"
                    v-for="n in 5 - language.level"
                    :key="n + language.level"
                  />
                </div>
              </li>
            </ul>
          </div>
        </div>
      </main>

      <section class="p-4 space-y-6 bg-gray-50 shadow-md md:col-span-2">
        <h2
          class="flex items-center space-x-4 text-2xl font-semibold text-gray-500"
        >
          <CodeIcon class="w-8 h-8 text-blue-500 stroke-2" />
          <span>Work Experience</span>
        </h2>
        <ul>
          <li
            class="py-4"
            v-for="work in data.workExperience"
            :key="work.start"
          >
            <h3 class="text-xl font-semibold text-gray-500">{{ work.role }}</h3>
            <div class="flex divide-x-2">
              <a
                class="pr-4 text-lg text-blue-700"
                :href="work.homepage"
                target="_blank"
                >{{ work.company }}</a
              >
              <div class="pl-4 flex items-center">
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
            </div>
            <p class="mt-2 text-black">{{ work.description }}</p>
          </li>
        </ul>
      </section>

      <section class="p-4 space-y-6 bg-gray-50 shadow-md md:col-span-2">
        <h2
          class="flex items-center space-x-4 text-2xl font-semibold text-gray-500"
        >
          <AcademicCapIcon class="w-8 h-8 text-blue-500 stroke-2" />
          <span>Education</span>
        </h2>
        <ul>
          <li
            class="py-4"
            v-for="station in data.education"
            :key="station.start"
          >
            <h3 class="text-xl font-semibold text-gray-500">
              {{ station.degree }}, {{ station.field }}
            </h3>
            <div class="flex divide-x-2">
              <a
                class="pr-4 text-lg text-blue-700"
                :href="station.homepage"
                target="_blank"
                >{{ station.location }}</a
              >
              <div class="pl-4 flex items-center">
                <CalendarIcon class="w-5 h-5 text-blue-500 stroke-2" />
                <span class="ml-2 text-blue-500"
                  >{{
                    station.start.toLocaleDateString("en-GB", {
                      year: "numeric",
                      month: "long",
                    })
                  }}
                  -
                  {{
                    station.end
                      ? station.end.toLocaleDateString("en-GB", {
                          year: "numeric",
                          month: "long",
                        })
                      : "Stopped"
                  }}</span
                >
              </div>
            </div>
            <p :v-if="station.description" class="mt-2 text-black">
              {{ station.description }}
            </p>
          </li>
        </ul>
      </section>

      <aside
        class="p-4 space-y-6 bg-gray-50 shadow-md md:col-span-4 lg:col-span-3"
      >
        <div>
          <h2
            class="flex items-center space-x-4 text-2xl font-semibold text-gray-500"
          >
            <PresentationChartIcon class="w-8 h-8 text-blue-500 stroke-2" />
            <span>Projects</span>
          </h2>
          <ul class="mt-4 md:grid md:grid-cols-4 md:gap-4">
            <li
              class="py-4"
              v-for="project in data.projects"
              :key="project.name"
            >
              <ProjectCard :project="project" />
            </li>
          </ul>
        </div>
      </aside>
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
import FlagIcon from "./components/icons/Flag.vue";
import PresentationChartIcon from "./components/icons/PresentationChart.vue";
import CodeIcon from "./components/icons/Code.vue";
import CalendarIcon from "./components/icons/Calendar.vue";
import AcademicCapIcon from "./components/icons/AcademicCap.vue";

import PageWidth from "./components/PageWidth.vue";
import ProjectCard from "./components/ProjectCard.vue";

import {data} from "./data";

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
    FlagIcon,
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
