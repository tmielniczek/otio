<template>
  <div class="realizations">
    <div
        v-if="currentProjectOverview < projectsOverviews.length-1"
        class="arrow arrow--right"
        @click="onArrowRightClick"></div>
    <div
        v-if="currentProjectOverview > 0"
        class="arrow arrow--left"
        @click="onArrowLeftClick"></div>
    <div class="grey-background" v-if="isProjectsOverviewVisible"></div>
    <div class="realization" v-if="isProjectsOverviewVisible">
      <div class="realization-header">Realizacje</div>
    </div>
    <div class="realization-content" v-if="isProjectsOverviewVisible">
      <div v-for="project of projectsOverviews" :key="project">
        <ProjectOverviewElement v-show="project.show"
                                :is-first-project="project.isFirstProject"
                                :is-project-not-animated="project.isProjectNotAnimated"
                                :is-fade-out-animation="project.isFadeOutAnimation"
                                :image-src="project.img"
                                @img-click="$emit('img-click')"
        ></ProjectOverviewElement>
      </div>
    </div>
  </div>
</template>

<script>
import ProjectOverviewElement from "@/components/ProjectOverviewElement";

export default {
  name: "ProjectsOverview",
  components: {ProjectOverviewElement},
  data: function () {
    return {
      isFirstProjectShow: true,
      projectsOverviews: [{
        id: 1, isFadeOutAnimation: false,
        isProjectNotAnimated: false,
        isFirstProject: true,
        show: true,
        img: require('@/assets/p2img1.png')
      },
        {
          id: 2,
          isFadeOutAnimation: false,
          isProjectNotAnimated: false,
          isFirstProject: false,
          show: false,
          img: require('@/assets/p2img2.png')
        },
        {
          id: 3,
          isFadeOutAnimation: false,
          isProjectNotAnimated: false,
          isFirstProject: false,
          show: false,
          img: require('@/assets/p2img3.png')
        },
      ],
      currentProjectOverview: 0,
      show: false,
      isProjectsOverviewVisible: false
    }
  }, mounted() {
    this.setIntersectionObserver(this.setSth);
  },
  methods: {
    setIntersectionObserver: function (callback) {
      let counter = 0;
      let options = {
        root: null,
        rootMargin: '0px',
        threshold: 0.7
      }

      let observer = new IntersectionObserver(() => {
        if (counter > 0) {
          callback()
        }
        counter++;
      }, options);

      observer.observe(document.getElementsByClassName('realizations')[0])
    },
    setSth() {
      this.isProjectsOverviewVisible = true;
    },
    onArrowRightClick() {
      this.projectsOverviews[this.currentProjectOverview].isFadeOutAnimation = true;
      setTimeout(() => {
        this.moveProjectsRight()
      }, 290)
    },
    moveProjectsRight: function () {
      this.projectsOverviews[this.currentProjectOverview].show = false;
      this.currentProjectOverview++;
      this.projectsOverviews[this.currentProjectOverview].isProjectNotAnimated = false;
      this.projectsOverviews[this.currentProjectOverview].show = true;
    },
    onArrowLeftClick() {
      this.projectsOverviews[this.currentProjectOverview].show = false;
      this.currentProjectOverview--;
      this.projectsOverviews[this.currentProjectOverview].isFadeOutAnimation = false;
      this.projectsOverviews[this.currentProjectOverview].isProjectNotAnimated = true;
      this.projectsOverviews[this.currentProjectOverview].show = true;
    }
  }
}
</script>

<style scoped>
@import "../styles/animation.css";

.arrow {
  border: solid black;
  border-width: 0 2px 2px 0;
  display: inline-block;
  padding: 2rem;
  cursor: pointer;
}

.arrow--right {
  position: absolute;
  bottom: 3rem;
  right: 3rem;
  transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
}

.arrow--left {
  position: absolute;
  bottom: 3rem;
  left: 3rem;
  z-index: 1;
  transform: rotate(135deg);
  -webkit-transform: rotate(135deg);
}

.realizations {
  height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: row;
  overflow: hidden;
  position: relative;
}

.realization-content {
  width: 85vw;
  height: 100%;
  margin: 10vh 7.5vw 10vh 7.5vw;
  position: relative;
}

.realization {
  position: absolute;
  bottom: -100vh;
  width: 5vw;
  height: 80vh;
  animation: slideInBottom 1s;
  animation-delay: .3s;
  animation-fill-mode: forwards;
  animation-timing-function: ease-out;
}

.realization-header {
  font-size: 2.4rem;
  font-weight: bold;
  transform: translateX(-100%) rotate(-90deg);
  transform-origin: right;
  text-transform: uppercase;
  letter-spacing: 3px;
  position: absolute;
  left: 2.5vw;
}

.grey-background {
  position: absolute;
  height: 85vh;
  background-color: lightgrey;
  width: 70vw;
  left: 5vw;
  z-index: -1;
  bottom: -100vh;
  animation: slideInBottom 1s;
  animation-delay: .3s;
  animation-fill-mode: forwards;
  animation-timing-function: ease-out;
}
</style>
