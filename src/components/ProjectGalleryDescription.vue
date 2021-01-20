<template>
  <div class="description"
       v-bind:style="{left: left, zIndex: zIndex}"
       v-bind:class="{galleryAnimateLeft: animateLeft, galleryAnimateRight: animateRight}">
    <div class="descriptions">
      <div class="background" v-bind:class="{backgroundAnimation: backgroundAnimation}"></div>
      <div class="description-header">P R O F I D E A - K R A K Ó W 2 0 2 0</div>
      <div class="description-body">Projekt i realizacja wyposażenia wnętrza
        showroom’u rowerowego. Lorem ipsum dolor sit
        amet, consectetur adipisicing elit, sed do
        eiusmod tempor incididunt ut labore et dolore
        magna aliqua. Ut enim ad minim veniam, quis
        nostrud exercitation ullamco laboris nisi ut
      </div>
      <div class="description-link">www.profidea.pl</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "GalleryDescription",
  props: ['left', 'animateLeft', 'animateRight', 'zIndex', 'backgroundAnimation'],
}
</script>

<style scoped>
.description {
  position: absolute;
  width: 100%;
  height: 100%;
}

.descriptions{
  width: 100%;
  height: 100%;
  background-color: white;
  padding: 3rem;
  position: absolute;
  backface-visibility: hidden;
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

.description-header {
  margin-top: 15rem;
  font-size: 2.4rem;
}

.description-body {
  backface-visibility: hidden;
  margin-top: 3rem;
  font-size: 1.6rem;
}

.description-link {
  margin-top: 3rem;
  font-size: 1.6rem;
}

.galleryAnimateLeft {
  transform: translateX(34vw);
  transition: transform 1.1s cubic-bezier(.7,0,.2,1);
}

.galleryAnimateRight {
  transform: translateX(-34vw);
  transition: transform 1.1s cubic-bezier(.7,0,.2,1);
}
</style>
