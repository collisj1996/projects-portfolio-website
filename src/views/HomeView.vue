<script lang="ts">
// eslint-disable-next-line import/extensions
import anime from 'animejs/lib/anime.es.js';
import { defineComponent, reactive, toRefs } from 'vue';
import ProjectList from '@/components/ProjectList.vue';
import NameTypographyStrokeSvg from '../components/NameTypographyStrokeSvg.vue';

export default defineComponent({
  name: 'HomeView',
  setup() {
    const state = reactive({
      landingSubheadingText: 'Full Stack Web Developer' as string,
      aboutTitle: 'About' as string,
      aboutSubheadingText: [
        'I\'m a career-driven and personable individual always looking to develop my portfolio of skills and experience.',
        `I have a bachelor's degree in Computer Science which has afforded me a solid understanding of computer theory; building upon
        this is my years working in the industry which has further developed my understanding into practical skills and knowledge.`,
      ] as string[],
      projectsTitle: 'Projects' as string,
      upTargetOffset: 0 as number,
      downTargetOffset: 0 as number,
      scrollDownCount: 0 as number,
    });
    return { ...toRefs(state) };
  },
  mounted() {
    this.setupScrollButtons();
    anime({
      targets: '#stroke-svg path',
      strokeDashoffset: [anime.setDashoffset, 0],
      easing: 'easeInOutSine',
      duration: 1500,
      delay(e: HTMLElement, i: number) { return i * 300; },
      direction: 'alternate',
      loop: false,
    });
  },
  methods: {
    setupScrollButtons() {
      this.downTargetOffset = document.getElementById('about-section')?.offsetHeight as number;

      document.addEventListener('scroll', () => {
        const { scrollTop } = document.documentElement;
        const aboutSection = document.getElementById('about-section') as HTMLElement;
        const projectsSection = document.getElementById('projects-section') as HTMLElement;

        // Scrolled past the landing section
        if (scrollTop >= aboutSection.offsetTop) {
          document.getElementById('scroll-button-up')?.classList.remove('hide');
          this.upTargetOffset = 0;
          this.downTargetOffset = projectsSection.offsetTop;
        } else {
          // bug here
          document.getElementById('scroll-button-up')?.classList.add('hide');
          this.downTargetOffset = aboutSection.offsetTop;
        }

        // Scrolled past the about section
        if (scrollTop >= projectsSection.offsetTop) {
          document.getElementById('scroll-button-down')?.classList.add('hide');
          this.upTargetOffset = aboutSection.offsetTop;
          // bug here
        } else {
          document.getElementById('scroll-button-down')?.classList.remove('hide');
        }

        if (this.scrollDownCount === 2) {
          this.upTargetOffset = document.getElementById('about-section')?.offsetHeight as number;
        }
      });

      const scrollButtonUp = document.getElementById('scroll-button-up') as HTMLElement;
      const scrollButtonDown = document.getElementById('scroll-button-down') as HTMLElement;

      scrollButtonUp.addEventListener('click', () => {
        this.scrollDownCount -= 1;
        window.scrollTo({
          top: this.upTargetOffset,
          behavior: 'smooth',
        });
        if (this.scrollDownCount < 2) {
          document.getElementById('scroll-button-down')?.classList.remove('hide-scroll-button');
        }
      });

      scrollButtonDown.addEventListener('click', () => {
        this.scrollDownCount += 1;
        window.scrollTo({
          top: this.downTargetOffset,
          behavior: 'smooth',
        });
        if (this.scrollDownCount === 2) {
          this.upTargetOffset = document.getElementById('about-section')?.offsetHeight as number;
          document.getElementById('scroll-button-down')?.classList.add('hide-scroll-button');
        }
      });
    },
  },
  components: {
    ProjectList,
    NameTypographyStrokeSvg,
  },
});
</script>

<template>
  <section id="landing-section">
    <div class="section-content">
      <div id="landing-content-container">
        <NameTypographySvg />
        <NameTypoBothSvg />
        <NameTypographyStrokeSvg />
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
    </div>
  </section>
  <section id="about-section">
    <div class="section-content">
      <div id="about-content-container">
        <div id="about-heading">{{ aboutTitle }}</div>
        <div id="about-content">
          <div id="about-left">
            <div id="about-subheading">
              <div class="about-paragraph" v-for="(paragraph, index) of aboutSubheadingText"
                :key="index">
                {{ paragraph }}
              </div>
            </div>
          </div>
          <div id="about-right">
            <div id="image-outer">
              <img id="about-photo" alt="Jack Collis Picture" src="../assets/myphotoupscaled.jpg">
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <section id="projects-section">
    <div class="section-content">
      <div class="absolute-title">{{ projectsTitle }}</div>
      <div id="projects-section-inner">
        <ProjectList />
      </div>
    </div>
  </section>
  <img id="scroll-button-up" class="scroll-button hide" alt="Scroll Up"
        src="../assets/icons8-up-arrow-64.png">
  <img id="scroll-button-down" class="scroll-button" alt="Scroll Down"
        src="../assets/icons8-down-arrow-64.png">
</template>

<style scoped>
#landing-section, #about-section, #projects-section {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  min-height: 100vh;
  overflow: hidden;
}

.section-content {
  width: 100%;
  max-width: 1200px;
  margin: clamp(100px, 10%, 200px) 12%;
}

#landing-section {
  background-color: var(--primary-color);
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

#scroll-button-up {
  top: 20px;
}

#scroll-button-down {
  bottom: 20px;
}

.scroll-button {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  font-size: 1.5rem;
  font-weight: bold;
  color: #fff;
  background: rgba(255, 255, 255, 0.178);
  cursor: pointer;
  text-decoration: none;
  padding: 5px;
  z-index: 999999;
  border-radius: 50%;
}

.scroll-button:hover {
  background: rgba(0, 0, 0, 0.089);
  border-radius: 50%;
}

#about-section {
  background-color: var(--primary-color);
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
  margin: 0 auto 50px 0;
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
  background-color: var(--primary-color);
}

#projects-section-inner {
  align-items: unset;
  padding: 20% 0 0 0;
  flex-direction: column;
  width: 100%;
}

.absolute-title {
  font-size: 3rem;
  font-weight: bold;
  margin: 0 0 50px 0;
  position: absolute;
}

#social-container {
  display: flex;
  justify-content: left;
  align-items: center;
  margin-top: 1rem;
}

.button-social {
  max-width: 32px;
  margin: 0 10px
}

.hide {
  display: none;
}

.hide-scroll-button {
  display: none;
}

.about-paragraph {
  margin: 0 0 2rem 0;
}

@media screen and (max-width: 1000px) {
  #about-content {
    flex-direction: column;
  }
}

@media screen and (max-width: 600px) {
  #projects-section-inner {
    padding: 100px 0 0 0;
  }
}
</style>
