<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue';
import ProjectList from '@/components/ProjectList.vue';

export default defineComponent({
  name: 'HomeView',
  setup() {
    const state = reactive({
      landingSubheadingText: 'Full Stack Web Developer' as string,
      aboutTitle: 'About' as string,
      aboutSubheadingText: 'I\'m a career-driven and personable individual always looking to develop my portfolio of skills and experience. I have a bachelor\'s degree in Computer Science which has afforded me a solid understanding of computer theory; building upon this is my years working in the industry which has further developed my understanding into practical skills and knowledge.' as string,
      projectsTitle: 'Projects' as string,
    });
    return { ...toRefs(state) };
  },
  mounted() {
    this.setupScrollButtons();
  },
  methods: {
    setupScrollButtons() {
      const landingScrollDown = document.getElementById('landing-section-scroll-down') as HTMLElement;
      const aboutScrollUp = document.getElementById('about-section-scroll-up') as HTMLElement;
      const aboutScrollDown = document.getElementById('about-section-scroll-down') as HTMLElement;
      const projectsScrollUp = document.getElementById('projects-section-scroll-up') as HTMLElement;
      const aboutSection = document.getElementById('about-section') as HTMLElement;
      landingScrollDown.addEventListener('click', () => {
        window.scrollTo({
          top: aboutSection.offsetHeight,
          behavior: 'smooth',
        });
      });
      aboutScrollUp.addEventListener('click', () => {
        window.scrollTo({
          top: 0,
          behavior: 'smooth',
        });
      });
      aboutScrollDown.addEventListener('click', () => {
        window.scrollTo({
          top: 2 * aboutSection.offsetHeight,
          behavior: 'smooth',
        });
      });
      projectsScrollUp.addEventListener('click', () => {
        window.scrollTo({
          top: aboutSection.offsetHeight,
          behavior: 'smooth',
        });
      });
    },
  },
  components: { ProjectList },
});
</script>

<template>
  <section id="landing-section">
    <div id="landing-content-container">
      <img alt="Jack Collis" src="../assets/name-typography.png">
      <div id="landing-subheading">{{ landingSubheadingText }}</div>
      <div id="social-container">
        <a href="https://github.com/collisj1996">
          <img class="button-social" alt="Github Social" src="../assets/GitHub-Mark-64px.png" >
        </a>
        <a href="https://www.linkedin.com/in/jack-collis-developer/">
          <img class="button-social" alt="LinkedIn Social" src="../assets/linked-in.png" >
        </a>
      </div>
    </div>
    <img id="landing-section-scroll-down" class="scroll-button" alt="Landing Down"
      src="../assets/icons8-down-arrow-64.png">
  </section>
  <section id="about-section">
    <img id="about-section-scroll-up" class="scroll-button" alt="Landing Down"
      src="../assets/icons8-up-arrow-64.png">
    <img id="about-section-scroll-down" class="scroll-button" alt="Landing Down"
      src="../assets/icons8-down-arrow-64.png">
    <div id="about-content-container">
      <div id="about-heading">{{ aboutTitle }}</div>
      <div id="about-content">
        <div id="about-left">
          <div id="about-subheading">
            {{ aboutSubheadingText }}
          </div>
        </div>
        <div id="about-right">
          <div id="image-outer">
            <img id="about-photo" alt="Jack Collis Picture" src="../assets/myphotoupscaled.jpg">
          </div>
        </div>
      </div>
    </div>
  </section>
  <section id="projects-section">
    <img id="projects-section-scroll-up" class="scroll-button" alt="Landing Down"
      src="../assets/icons8-up-arrow-64.png">
    <div class="absolute-title">{{ projectsTitle }}</div>
    <div id="projects-section-inner">
      <ProjectList />
    </div>
  </section>
</template>

<style scoped>
#landing-section, #about-section, #projects-section {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

#landing-section {
  background-color: var(--primary-color);
  height: 100vh;
}

#landing-content-container {
  display: flex;
  justify-content: center;
  flex-direction: column;
}

#landing-subheading {
  margin: 20px 0 0 0;
  font-size: 1.5rem;
  font-weight: bold;
}

#landing-section-scroll-down, #about-section-scroll-down {
  bottom: 20px;
}

#about-section-scroll-up, #projects-section-scroll-up {
  top: 20px;
}

.scroll-button {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  font-size: 1.5rem;
  font-weight: bold;
  color: #fff;
  cursor: pointer;
  text-decoration: none;
  padding: 5px;
}

.scroll-button:hover {
  background: rgba(0, 0, 0, 0.089);
  border-radius: 50%;
}

#about-section {
  background-color: var(--secondary-color);
  height: 100vh;
}

#about-left {
  flex: 1 1 60%
}

#about-right {
  flex: 1 1 40%;
  padding: 1rem 0;
}

#image-outer {
  max-width: 220px;
  max-height: 220px;
  overflow: hidden;
  border-radius: 50%;
  margin: 0 auto;
}

#about-heading {
  font-size: 3rem;
  font-weight: bold;
  margin: 0 0 50px 0;
}

#about-subheading {
  margin: 20px 0 0 0;
  font-size: 1.5rem;
}

#about-content-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  margin: 0 10%;
  min-width: 500px;
}

#about-content {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
}

#about-photo {
  height: 100%;
  width: 100%;
  transform: translate(0,-10px) scale(1.2);
}

#projects-section {
  background-color: var(--tertiary-color);
  min-height: 100vh;
}

#projects-section-inner {
  align-items: unset;
  padding: 50vh 10% 0 10%;
  flex-direction: column;
  width: 100%;
}

.absolute-title {
  font-size: 3rem;
  font-weight: bold;
  margin: 0 0 50px 0;
  position: absolute;
  top: 25vh;
}

#social-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1rem;
}

.button-social {
  max-width: 32px;
  margin: 0 10px
}

@media screen and (max-width: 1000px) {
  #about-content {
    flex-direction: column;
  }
}
</style>
