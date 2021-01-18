<template>
  <div style="width: 100%; height: 100vh" class="project-gallery">
    <div class="previous-page">nastepna strona</div>
    <div class="next-page">poprzednia strona</div>
    <div class="gallery">
      <div class="one-image-row">
        <img src="../assets/p2img1.png">
      </div>
      <div class="two-image-row">
        <img src="../assets/p5imgvertical.png">
        <img src="../assets/p5imgvertical.png">
      </div>
      <div></div>
    </div>
    <div class="description">
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
  name: "Project"
}
</script>

<style scoped>
.project-gallery {
  position: relative;
  display: flex;
  flex-direction: row;
}

.next-page {
  position: absolute;
}

.previous-page {
  position: absolute;
}

.gallery {
  overflow: hidden;
  overflow-y: scroll;
  padding: 3vw 3vw;
  width: 66vw;
  height: inherit;
  background-color: grey;
}

.gallery::-webkit-scrollbar {
  display: none;
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

.description {
  margin-top: 15rem;
  height: inherit;
  width: 34vw;
  background-color: white;
  padding: 3rem;
}

.description-header {
  font-size: 2.4rem;
}

.description-body {
  margin-top: 3rem;
  font-size: 1.6rem;
}

.description-link {
  margin-top: 3rem;
  font-size: 1.6rem;
}
</style>
