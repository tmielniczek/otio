<template>
  <div class="home" id="home" v-bind:class="{homeOverflowHidden: homeOverflowHidden}">
    <div class="background" v-bind:class="{backgroundAnimation: backgroundAnimation}" ref="homeBackground"></div>
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
      homeOverflowHidden: false,
      backgroundAnimation: false,
      translateXValue: null
    }
  },
  mounted() {
    window.onpopstate = () => {
      this.$refs.projectGallery.style.transform = `translateY(${this.translateXValue}px)`;
      this.$refs.projectGallery.style.transition = 'transform 1s cubic-bezier(.7, 0, .2, 1)';
      setTimeout(()=>{
        this.isProject = false;
        this.homeOverflowHidden = false;
      }, 900)
    }
  },
  methods: {
    onImageClick() {
      history.pushState(null, null, 'gallery')
      this.homeOverflowHidden = true;
      this.isProject = true;
      this.$refs.homeBackground.style.top = -1 * document.getElementsByClassName('page-two')[0].getBoundingClientRect().top + 'px';
      this.backgroundAnimation = true;
      setTimeout(() => {
        this.$refs.projectGallery.ontransitionend = () => {
          this.backgroundAnimation = false;
        }
        this.translateXValue = window.innerHeight + document.getElementsByClassName('realizations')[0].getBoundingClientRect().top;
        this.$refs.projectGallery.style.transform = `translateY(-${this.translateXValue}px)`;
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

.background {
  left: 0;
  top: 0;
  opacity: 0;
  background-color: rgba(0, 0, 0, .2);
  position: absolute;
  width: 100%;
  height: 100%;
}

.backgroundAnimation {
  opacity: 1;
  transition: opacity .3s cubic-bezier(.68, 0, .42, 1);
}
</style>
