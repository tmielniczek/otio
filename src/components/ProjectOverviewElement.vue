<template>
  <div class="project-overview"
       v-bind:class="{'project-overview--animated': !isFirstProject,
       'project-overview--not-animated': isProjectNotAnimated,
       'project-overview--fade-out': isFadeOutAnimation
       }">
    <div class="page-item page-item--left">
      <div class="img-wrapper">
        <img class="item-img" :src="imageSrc" @click="$emit('img-click')" ref="itemImgLeft">
      </div>
      <div class="text-box">
        <div class="text-header-wrapper">
          <div class="text-header text-header-first text-header---left"
               v-bind:class="!isFirstProject || isProjectNotAnimated ? 'text-header-first--no-animation' : ''">PRODIFEA
            KRAKOW 2020
          </div>
        </div>
        <div class="text-wrapper">
          <div class="text text-first text--left"
               v-bind:class="!isFirstProject || isProjectNotAnimated ? 'text-first--no-animation' : ''">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aspernatur beatae culpa
            cupiditate doloribus eaque fugiat hic laborum modi molestiae neque nihil nobis, non nulla
            obcaecati
            provident quos sapiente suscipit voluptatibus?
          </div>
        </div>
      </div>
    </div>
    <div class="page-item page-item--right">
      <div class="page-item-content">
        <div class="text-box">
          <div class="text-header-wrapper text-header-wrapper--right">
            <div class="text-header text-header-first text-header---right"
                 v-bind:class="!isFirstProject || isProjectNotAnimated ? 'text-header-first--no-animation ' : ''"
            >PRODIFEA KRAKOW 2020
            </div>
          </div>
          <div class="text-wrapper">
            <div class="text text-first text--right"
                 v-bind:class="!isFirstProject || isProjectNotAnimated ? 'text-first--no-animation' : ''">
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aspernatur beatae culpa
              cupiditate doloribus eaque fugiat hic laborum modi molestiae neque nihil nobis, non nulla
              obcaecati
              provident quos sapiente suscipit voluptatibus?
            </div>
          </div>
        </div>
        <div class="img-wrapper">
          <img class="item-img" :src="imageSrc" ref="itemImgRight">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProjectOverviewElement",
  props: ['isFirstProject', 'isProjectNotAnimated', 'isFadeOutAnimation', 'imageSrc'],
  data: function () {
    return {}
  },
  mounted() {
    this.$refs.itemImgLeft.ontransitionend = () => {
      this.$refs.itemImgLeft.style.transitionDelay = '0s';
    }
    this.$refs.itemImgRight.ontransitionend = () => {
      this.$refs.itemImgRight.style.transitionDelay = '0s';
    }
    setTimeout(() => {
      const imageItemCollection = document.getElementsByClassName('item-img');
      Array.from(imageItemCollection).forEach(el => {
        el.style.maxWidth = '33vw';
      })
    }, 100)
  }
}
</script>

<style scoped>
.project-overview {
  position: absolute;
  display: flex;
  flex-direction: column;
}

.project-overview--animated {
  animation: slideInPageThreeNextFromLeft 1s;
  animation-fill-mode: forwards;
  animation-timing-function: ease-out;
}

.project-overview--not-animated {
  animation: none;
}

.project-overview--fade-out {
  animation: fadeOut .3s ease-in-out;
}

.page-item {
  display: flex;
  height: 40vh;
  position: relative;
}

.page-item-content {
  display: flex;
  position: absolute;
  left: 12vw;
}

.item-img {
  height: 40vh;
  display: block;
  max-width: 0;
  transition: all 1s;
  transition-delay: 1.2s;
  cursor: pointer;
}

.item-img:hover {
  transform: scale(1.1);
}

.img-wrapper {
  height: 100%;
  max-width: 33vw;
  overflow: hidden;
}

.text-header {
  height: 30px;
  width: 30vw;
  position: absolute;
  right: 30vw;
  opacity: 0;
  font-size: 24px;
  letter-spacing: 6px;
}

.text-header---left {
  padding-left: 3vw;
}

.text-header---right {
  text-align: right;
  padding-right: 3vw;
  width: 40vw;
}

.text-header-first {
  animation: slideInTextHeaderFromLeft 1s;
  animation-delay: 1.3s;
  animation-fill-mode: forwards;
}

.text-header-first--no-animation {
  animation: none;
  opacity: 1;
  right: 0;
}

.text-header-wrapper {
  height: 30px;
  width: 30vw;
  overflow: hidden;
  position: relative;
  margin-bottom: 3rem;
}

.text-header-wrapper--right {
  width: 40vw;
}

.text-box {
  margin-top: 7vh;
  width: 40vw;
  position: relative;
  margin-left: 10px;
}

.text-wrapper {
  width: 30vw;
  position: relative;
}

.text {
  font-family: Roboto, sans-serif;
  width: 40vw;
  position: absolute;
  top: 0;
  left: 33vw;
  opacity: 0;
  z-index: -1;
  font-size: 1.6vh;
  letter-spacing: 1px;
  line-height: 3vh;
}

.text-first {
  animation: slideInTextFromRight 1s;
  animation-delay: 1.5s;
  animation-fill-mode: forwards;
}

.text-first--no-animation {
  animation: none;
  opacity: 1;
  left: 0;
}

.text--left {
  padding-left: 5vw;
}

.text--right {
  text-align: right;
  padding-right: 5vw;
}

@keyframes fadeOut {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}

@keyframes slideInTextFromRight {
  0% {
    opacity: 0;
    left: 30vw;
  }
  100% {
    opacity: 1;
    left: 0;
  }
}

@keyframes slideInTextHeaderFromLeft {
  0% {
    opacity: 0;
    right: 30vw;
  }
  100% {
    opacity: 1;
    right: 0;
  }
}

@keyframes slideInPageThreeNextFromLeft {
  0% {
    left: 80vw;
  }
  100% {
    left: 0;
  }
}
</style>
