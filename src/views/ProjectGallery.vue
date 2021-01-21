<template>
  <div style="width: 100%; height: 100vh" class="project-gallery">
    <div class="page-btn previous-page" @click="nextPage" v-if="currentProjectIndex < galleries.length-1">nastepna
      strona
    </div>
    <div class="page-btn next-page" @click="previousPage" v-if="currentProjectIndex > 0">poprzednia strona</div>
    <div class="project-gallery-images-wrapper">
      <div v-for="(gallery, index) of galleries" :key="index">
        <ProjectGalleryImages
            :left="gallery.left === 0 ? gallery.left : gallery.left + 'vw'"
            :animate-left="gallery.animateLeft"
            :animate-right="gallery.animateRight"
            :z-index="gallery.zIndex"
            :background-animation="gallery.backgroundAnimation"
        ></ProjectGalleryImages>
      </div>
    </div>
    <div class="project-gallery-desc-wrapper">
      <div v-for="(desc, index) of descriptions" :key="index">
        <ProjectGalleryDescription
            :left="desc.left === 0 ? desc.left : desc.left + 'vw'"
            :animate-left="desc.animateLeft"
            :animate-right="desc.animateRight"
            :z-index="desc.zIndex"
            :background-animation="desc.backgroundAnimation"
        ></ProjectGalleryDescription>
      </div>
    </div>
  </div>
</template>

<script>
import ProjectGalleryImages from "@/components/ProjectGalleryImages";
import ProjectGalleryDescription from "@/components/ProjectGalleryDescription";

export default {
  name: "ProjectGallery",
  components: {ProjectGalleryImages, ProjectGalleryDescription},
  data: function () {
    return {
      currentProjectIndex: 0,
      galleries: [{show: true, left: 0, animateLeft: false, animateRight: false, zIndex: 5, backgroundAnimation: false},
        {show: true, left: 66, animateLeft: false, animateRight: false, zIndex: 5, backgroundAnimation: false},
        {show: true, left: 132, animateLeft: false, animateRight: false, zIndex: 5, backgroundAnimation: false}
      ],
      descriptions: [
        {show: true, left: 0, animateLeft: false, animateRight: false, zIndex: 5, backgroundAnimation: false},
        {show: true, left: 34, animateLeft: false, animateRight: false, zIndex: 5, backgroundAnimation: false},
        {show: true, left: 68, animateLeft: false, animateRight: false, zIndex: 5, backgroundAnimation: false}
      ],
      zIndex: 5,
      isAnimationOngoing: false
    }
  },
  methods: {
    nextPage() {
      if (!this.isAnimationOngoing) {
        this.isAnimationOngoing = true;
        this.currentProjectIndex++;
        this.galleries[this.currentProjectIndex - 1].backgroundAnimation = true;
        this.galleries[this.currentProjectIndex].animateRight = true;
        this.galleries[this.currentProjectIndex].zIndex = ++this.zIndex;
        this.descriptions[this.currentProjectIndex - 1].backgroundAnimation = true;
        this.descriptions[this.currentProjectIndex].animateRight = true;
        this.descriptions[this.currentProjectIndex].zIndex = ++this.zIndex;
        setTimeout(() => {
          this.galleries.forEach(gallery => {
            gallery.left = gallery.left - 66;
          })
          this.descriptions.forEach(desc => {
            desc.left = desc.left - 34;
          })
          this.galleries[this.currentProjectIndex - 1].backgroundAnimation = false;
          this.descriptions[this.currentProjectIndex - 1].backgroundAnimation = false;
          this.galleries[this.currentProjectIndex].animateRight = false;
          this.descriptions[this.currentProjectIndex].animateRight = false;
          this.isAnimationOngoing = false;
        }, 1100)
      }
    },
    previousPage() {
      if (!this.isAnimationOngoing) {
        this.isAnimationOngoing = true;
        this.currentProjectIndex--;
        this.galleries[this.currentProjectIndex].animateLeft = true;
        this.galleries[this.currentProjectIndex + 1].backgroundAnimation = true;
        this.galleries[this.currentProjectIndex].zIndex = ++this.zIndex;
        this.descriptions[this.currentProjectIndex].animateLeft = true;
        this.descriptions[this.currentProjectIndex + 1].backgroundAnimation = true;
        this.descriptions[this.currentProjectIndex].zIndex = ++this.zIndex;
        setTimeout(() => {
          this.galleries.forEach(gallery => {
            gallery.left = gallery.left + 66;
          })
          this.descriptions.forEach(desc => {
            desc.left = desc.left + 34;
          })
          this.galleries[this.currentProjectIndex + 1].backgroundAnimation = false;
          this.descriptions[this.currentProjectIndex + 1].backgroundAnimation = false;
          this.galleries[this.currentProjectIndex].animateLeft = false;
          this.descriptions[this.currentProjectIndex].animateLeft = false;
          this.isAnimationOngoing = false;
        }, 1100)
      }
    }
  }
}
</script>

<style scoped>
@import "../styles/animation.css";

.project-gallery {
  position: relative;
  display: flex;
  flex-direction: row;
}

.page-btn {
  cursor: pointer;
  font-weight: bold;
  transform-origin: right;
  font-size: 2rem;
  text-transform: uppercase;
  position: absolute;
  z-index: 20000;
  backface-visibility: hidden;
}

.next-page {
  display: inline-block;
  top: 60vh;
  transform: translateX(-100%) rotate(-90deg);
  left: 1vw;
}

.previous-page {
  display: inline-block;
  top: 73vh;
  transform: translateX(-100%) rotate(-270deg);
  white-space: nowrap;
  left: 99vw;
}

.project-gallery-images-wrapper {
  overflow: scroll;
  width: 66vw;
  height: inherit;
  position: relative;
  display: flex;
  flex-direction: row;
}

.project-gallery-images-wrapper::-webkit-scrollbar {
  display: none;
}

.project-gallery-desc-wrapper {
  overflow: hidden;
  width: 34vw;
  height: inherit;
  position: relative;
}
</style>
