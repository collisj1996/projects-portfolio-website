<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue';

export default defineComponent({
  name: 'ProjectList',
  setup() {
    // eslint-disable-next-line no-shadow
    enum ProjectStatus {
      Ongoing = 'Ongoing',
      Inactive = 'Inactive',
      Finished = 'Finished',
    }

    interface Project {
      name: string;
      description: string[];
      image: string;
      githubLink: string;
      demoLink: string;
      pageLink: string;
      status: ProjectStatus;
      tags: string[];
    }

    const state = reactive({
      projects: [
        {
          name: 'Algo Sandbox',
          description: [
            'A visual sandbox to test path finding algorithms and more...',
            'An ongoing project',
          ],
          image: 'algo-sandbox.png',
          githubLink: 'https://github.com/collisj1996/algo-sandbox',
          demoLink: '',
          pageLink: '',
          status: ProjectStatus.Ongoing,
          tags: ['JavaScript', 'TypeScript', 'Vue 3', 'Composition API', 'Alogrithms', 'Pathfinding', 'Visualization'],
        },
        {
          name: 'Portfolio',
          description: [
            'High quality, responsive, and user-friendly portfolio website',
            'An ongoing project',
          ],
          image: '',
          githubLink: '',
          demoLink: '',
          pageLink: '',
          status: ProjectStatus.Ongoing,
          tags: ['JavaScript', 'TypeScript', 'Vue 3', 'Composition API', 'UI', 'UX', 'Responsive'],
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
          pageLink: '',
          status: ProjectStatus.Finished,
          tags: ['JavaScript', 'Vue 2', 'Vuex', 'Full Stack', 'Serverless', 'AWS', 'MySQL', 'SQS', 'EC2', 'NodeJS', 'Lambda', 'RDS'],
        },
        {
          name: 'Game of Life',
          description: ['A recreation of Conway\'s Game of Life in Javscript'],
          image: 'game-of-life.png',
          githubLink: 'https://github.com/collisj1996/Game-of-Life',
          demoLink: 'https://collisj1996.github.io/Game-of-Life/',
          pageLink: '',
          status: ProjectStatus.Finished,
          tags: ['JavaScript', 'Algorithms', 'MVC', 'Visualization'],
        },
        {
          name: 'Raycasting',
          description: ['A visualisation of a simple 2D "raycasting" algorithm'],
          image: 'raycasting.png',
          githubLink: 'https://github.com/collisj1996/Raycasting',
          demoLink: 'https://collisj1996.github.io/Raycasting/',
          pageLink: '',
          status: ProjectStatus.Finished,
          tags: ['JavaScript', 'Algorithms', 'Interactive', 'Visualization'],
        },
        {
          name: 'Memory Jar',
          description: ['An android based mobile application developed to help people with dementia to remember things, based on the premise of positive reminiscemence.'],
          image: 'memory-jar.png',
          githubLink: 'https://github.com/collisj1996/MemoryJar',
          demoLink: '',
          pageLink: '',
          status: ProjectStatus.Finished,
          tags: ['Java', 'Android', 'Mobile'],
        },
        {
          name: 'Conversion Toolkit',
          description: [
            'The Conversion Toolkit mobile application for Android provides users with an easy-to-use "toolkit" for day to day conversions. Whether you are trying to convert Kilometers to Miles, understand the amount of Electronvolts in a Joule or see how many Indian Rupees you can get for 50 British Pounds, Conversion Toolkit can do it all',
          ],
          image: 'conversion-toolkit.png',
          githubLink: 'https://github.com/collisj1996/Unit-Conversion-Tool',
          demoLink: 'https://play.google.com/store/apps/details?id=com.arcticumi.Conversion_Toolkit&hl=en_US',
          pageLink: '',
          status: ProjectStatus.Finished,
          tags: ['Java', 'Android', 'Mobile'],
        },
      ] as Project[],
    });

    return { ...toRefs(state) };
  },
  methods: {
    getImage(imageUrl: string) {
      // eslint-disable-next-line import/no-dynamic-require, global-require
      return require(`@/assets/${imageUrl}`);
    },
  },
});
</script>

<template>
  <div class="project-card" v-for="(project, index)
    of projects" :key="index">
    <div class="project-card-content">
      <div class="project-card-name">{{ project.name }} | {{ project.status }}</div>
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
      <div class="project-tags">
        <div class="project-tag" v-for="(tag, index) of project.tags" :key="index">
          {{ tag }}
        </div>
      </div>
    </div>
    <img v-if="project.image" class="project-card-image" alt="" :src="getImage(project.image)">
  </div>
</template>

<style scoped>
.project-card {
  display: flex;
  flex: 1 1 50%;
  flex-direction: row;
  height: fit-content;
  background: white;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  padding: 1rem;
  position: relative;
  max-width: 1200px;
  margin: 0 auto 3rem auto;
}

.project-card:hover {
}

.project-card-name {
  display: flex;
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

.project-tags {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 0.5rem;
  margin-top: 1rem;
  flex-wrap: wrap;
}

.project-tag {
  border-radius: 5px;
  padding: 0.5rem 1rem;
  white-space: nowrap;
  color: white;
  background: rgb(53, 53, 53);
}

@media (max-width: 880px) {
  .project-card-image {
    display: none;
  }
}
</style>
