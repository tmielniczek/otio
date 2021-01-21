<template>
  <div class="home" id="home" v-bind:class="{homeOverflowHidden: homeOverflowHidden}">
    <TitlePage></TitlePage>
    <ProjectsOverview @img-click="onImageClick"></ProjectsOverview>
    <div class="home__project" v-if="isProject" ref="projectGallery">
      <ProjectGallery></ProjectGallery>
    </div>
  </div>
</template>

<script>
import ProjectsOverview from "@/components/ProjectsOverview";
import ProjectGallery from "@/views/ProjectGallery";
import TitlePage from "@/components/TitlePage";

export default {
  name: "Main",
  components: {TitlePage, ProjectGallery, ProjectsOverview},
  data: function () {
    return {
      isProject: false,
      homeProjectAnimate: false,
      homeOverflowHidden: false
    }
  },
  methods: {
    onImageClick() {
      this.homeOverflowHidden = true;
      window.onpopstate = () => {
        this.isProject = false;
      }
      this.isProject = true;
      setTimeout(() => {
        let translateXValue = window.innerHeight +  document.getElementsByClassName('realizations')[0].getBoundingClientRect().top;
        this.$refs.projectGallery.style.transform = `translateY(-${translateXValue}px)`;
        this.$refs.projectGallery.style.transition = 'transform 1s cubic-bezier(.7, 0, .2, 1)';
        this.homeProjectAnimate = true
      }, 10)
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
  overflow: scroll;
}

.homeOverflowHidden {
  overflow: hidden;
}

.home::-webkit-scrollbar {
  display: none;
}

.home__project {
  position: absolute;
  z-index: 2;
  bottom: -200vh;
}

.homeProjectAnimate {
  transform: translateY(-1500px);
  transition: transform 1s cubic-bezier(.7, 0, .2, 1);
}
</style>
