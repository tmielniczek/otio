<template>
  <div class="home">
    <ProjectsOverview @img-click="onImageClick" v-if="isProject"></ProjectsOverview>
    <Project class="home__project"></Project>
  </div>
</template>

<script>
import ProjectsOverview from "@/components/ProjectsOverview";
import Project from "@/views/ProjectGallery";

export default {
  name: "Main",
  components: {Project, ProjectsOverview},
  data: function () {
    return {
      isProject: false
    }
  },
  methods: {
    onImageClick() {
      window.onpopstate = () => {
        this.isProject = false;
      }
      this.isProject = true;
    }
  }
}
</script>

<style scoped>
@import "../styles/animation.css";

.home {
  height: 100vh;
  width: 100%;
  position: relative;
  overflow: hidden;
}

.home__project {
  position: absolute;
  z-index: 2;
  animation: slideInBottom 1s;
  animation-fill-mode: forwards;
  animation-timing-function: ease-out;
}
</style>
