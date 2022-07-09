<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue';

export default defineComponent({
  name: 'ProjectList',
  setup() {
    interface Project {
      name: string;
      description: string[];
      image: string;
      githubLink: string;
      demoLink: string;
    }

    const state = reactive({
      projects: [
        {
          name: 'Algo Sandbox',
          description: [
            'A visual sandbox to test path finding algorithms and more...',
            'Currently still under development',
          ],
          image: 'algo-sandbox.png',
          githubLink: 'https://github.com/collisj1996/algo-sandbox',
          demoLink: '',
        },
        {
          name: 'Minecraft Server Hub',
          description: [
            'A server hub for users to browse, upload, and vote on their favourite servers.',
            `As my biggest project, this was an end-to-end solution, including a VUE2 frontend,
            a serverless NodeJS backend using AWS Lambda, and a MySQL database hosted on AWS RDS.`,
            `Whilst the project is no longer active due to heavy running costs, I do one day want to
            pick up this project again.`],
          image: 'msh.png',
          githubLink: 'https://github.com/collisj1996/minecraft-server-hub-frontend',
          demoLink: '',
        },
        {
          name: 'Game of Life',
          description: ['A recreation of Conway\'s Game of Life in Javscript'],
          image: 'game-of-life.png',
          githubLink: 'https://github.com/collisj1996/Game-of-Life',
          demoLink: 'https://collisj1996.github.io/Game-of-Life/',
        },
        {
          name: 'Raycasting',
          description: ['A visualisation of a simple 2D "raycasting" algorithm'],
          image: 'raycasting.png',
          githubLink: 'https://github.com/collisj1996/Raycasting',
          demoLink: 'https://collisj1996.github.io/Raycasting/',
        },
        {
          name: 'Memory Jar',
          description: ['An android based mobile application developed to help people with dementia to remember things, based on the premise of positive reminiscemence.'],
          image: 'algo-sandbox.png',
          githubLink: 'https://github.com/collisj1996/MemoryJar',
          demoLink: '',
        },
        {
          name: 'Conversion Toolkit',
          description: [
            'The Conversion Toolkit mobile application for Android provides users with an easy-to-use "toolkit" for day to day conversions. Whether you are trying to convert Kilometers to Miles, understand the amount of Electronvolts in a Joule or see how many Indian Rupees you can get for 50 British Pounds, Conversion Toolkit can do it all',
          ],
          image: 'algo-sandbox.png',
          githubLink: 'https://github.com/collisj1996/Unit-Conversion-Tool',
          demoLink: 'https://play.google.com/store/apps/details?id=com.arcticumi.Conversion_Toolkit&hl=en_US',
        },
        {
          name: 'Calculator',
          description: [
            'A simple calculator application that can perform basic arithmetic operations.',
          ],
          image: 'algo-sandbox.png',
          githubLink: 'https://github.com/collisj1996/Calculator',
          demoLink: 'https://play.google.com/store/apps/details?id=com.arcticumi.calculator&hl=en_GB',
        },
      ] as Project[],
    });

    return { ...toRefs(state) };
  },
  methods: {
    getProjectCardClass(index: number) {
      return index % 2 === 0 ? 'project-card-left' : 'project-card-right';
    },
    getImage(imageUrl: string) {
      // eslint-disable-next-line import/no-dynamic-require, global-require
      return require(`@/assets/${imageUrl}`);
    },
  },
});
</script>

<template>
  <div :class="getProjectCardClass(index)" class="project-card" v-for="(project, index) of projects"
    :key="index">
    <div class="project-card-content">
      <div class="project-card-name">{{ project.name }}</div>
      <div class="project-card-description">
        <div class="project-card-paragraph" v-for="(paragraph, index) of project.description"
          :key="index">
          {{ paragraph }}
        </div>
      </div>
      <div class="project-links">
        <a :href="project.githubLink" target="_blank" rel="noopener noreferrer">
          Project Code
          <img src="https://img.icons8.com/color/48/000000/github.png" alt="Github" />
        </a>
        <a v-if="project.demoLink" :href="project.demoLink" target="_blank"
          rel="noopener noreferrer">
          Project Demo
          <img src="https://img.icons8.com/color/48/000000/play.png" alt="Demo" />
        </a>
      </div>
    </div>
    <img class="project-card-image" alt="" :src="getImage(project.image)">
  </div>
</template>

<style scoped>
.project-card {
  display: flex;
  flex-direction: row;
  height: fit-content;
  width: 80%;
  max-width: 800px;
  background: white;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  padding: 1rem;
  margin-bottom: 3rem;
  position: relative;
}

.project-card-name {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.project-card-content {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.project-card-description {
  text-align: left;
  font-size: 1rem;
  margin-bottom: 0.5rem;
  width: 100%;
}

.project-card-image {
  width: 150px;
  height: 150px;
  object-fit: cover;
  margin-left: 1rem;
  align-self: center;
}

.project-card-left {
  margin-right: auto;
}

.project-card-right {
  margin-left: auto;
}

#current-project-image {
  position: absolute;
  top: 0;
  right: 0;
  transform: translate(50%, -50%);
  max-width: 200px;
  padding: 5px 20px;
  background: white;
  border: 2px solid black;
  border-radius: 10px;
}

.project-card-paragraph {
  margin-bottom: 0.5rem;
}

.project-links {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 0.5rem;
}

.project-links a {
  text-decoration: none;
  color: black;
  display: flex;
  justify-content: center;
  align-items: center;
}

.projects-links a img {
  margin-left: 0.5rem;
}
</style>
