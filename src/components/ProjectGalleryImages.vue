<template>
  <div class="gallery"
       v-bind:style="{left: left, zIndex: zIndex}"
       v-bind:class="{galleryAnimateLeft: animateLeft, galleryAnimateRight: animateRight}">
    <div class="images">
      <div class="background" v-bind:class="{backgroundAnimation: backgroundAnimation}"></div>
      <div class="one-image-row">
        <img src="../assets/p2img1.png">
      </div>
      <div class="two-image-row">
        <img src="../assets/p5imgvertical.png">
        <img src="../assets/p5imgvertical.png">
      </div>
      <div></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Gallery",
  props: ['left', 'animateLeft', 'animateRight', 'zIndex', 'backgroundAnimation'],
  mounted() {
  },
  methods: {}
}
</script>

<style scoped>
.gallery {
  position: absolute;
}

.images {
  padding: 3vw 3vw;
  width: 100%;
  background-color: grey;
  height: fit-content;
  position: relative;
}

.background {
  left: 0;
  top: 0;
  opacity: 0;
  background-color: rgba(0,0,0,0.2);
  z-index: 30;
  position: absolute;
  width: 100%;
  height: 100%;
}

.backgroundAnimation {
  opacity: 1;
  transition: opacity .3s cubic-bezier(.68,0,.42,1);
}

.galleryAnimateLeft {
  transform: translateX(66vw);
  transition: transform 1.1s cubic-bezier(.7,0,.2,1);
}

.galleryAnimateRight {
  transform: translateX(-66vw);
  transition: transform 1.1s cubic-bezier(.7,0,.2,1);
}

.one-image-row {
  padding-bottom: 3vw;
}

.one-image-row img {
  width: 60vw;
}

.two-image-row {
  display: flex;
  justify-content: space-between;
  padding-bottom: 3vw;
}

.two-image-row img {
  width: 29vw;
}
</style>
