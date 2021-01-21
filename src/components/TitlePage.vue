<template>
  <div class="title-page" ref="titlePage">
    <div class="title-page-logo" ref="titlePageLogo">
      OTIO
    </div>
  </div>
  <div class="page-two" ref="pageTwo">
    <div class="scroll-btn" @click="onScrollButtonClick">SCROLL</div>
  </div>
</template>

<script>
export default {
  name: "TitlePage",
  mounted() {
    this.$refs.titlePageLogo.addEventListener('animationend', () => {
      this.$refs.titlePage.style.display = 'none';
      this.$refs.pageTwo.style.display = 'block';
    });
  },
  methods: {
    onScrollButtonClick() {
      let scrollDistance = document.documentElement.clientHeight;
      document.getElementsByClassName('home')[0].scrollBy({
        top: scrollDistance,
        behavior: "smooth"
      });
    }
  }
}
</script>

<style scoped>
.title-page {
  height: 100vh;
  width: 100%;
  position: relative;
}

.title-page-logo {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
  margin: 0 auto;
  width: fit-content;
  font-size: 36px;
  animation: fadein .5s;
}

.page-two {
  display: none;
  height: 100vh;
  width: 100%;
  background-image: url("../assets/otio-2.png");
  background-repeat: no-repeat;
  background-size: cover;
  animation: fadein .5s;
}

.scroll-btn {
  position: absolute;
  top: calc(100vh - 50px);
  left: 50vw;
  transform: translateX(-50%);
  cursor: pointer;
}


@keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
