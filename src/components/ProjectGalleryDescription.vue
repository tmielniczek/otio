<template>
  <div class="description"
       v-bind:style="{left: left, zIndex: zIndex}"
       v-bind:class="{galleryAnimateLeft: animateLeft, galleryAnimateRight: animateRight}">
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
</template>

<script>
export default {
  name: "GalleryDescription",
  props: ['left', 'animateLeft', 'animateRight', 'zIndex'],
}
</script>

<style scoped>
.description {
  width: 100%;
  margin-top: 15rem;
  background-color: white;
  padding: 3rem;
  position: absolute;
  backface-visibility: hidden;
}

.description-header {
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
  transition: transform 1.1s cubic-bezier(.68,0,.42,1);
}

.galleryAnimateRight {
  transform: translateX(-34vw);
  transition: transform 1.1s cubic-bezier(.68,0,.42,1);
}
</style>
