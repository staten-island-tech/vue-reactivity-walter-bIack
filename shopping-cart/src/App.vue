<script>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
    <img src="./assets/background.webp" class="background" />
  <RouterView class="view"/>
</template>

<style scoped>
.view {
  height: calc(100vh - 5rem);

}
header {
  line-height: 1.5;
}

nav {
  padding-top: 0.5rem;
  height: 3rem;
  width: 100%;
  font-size: 16px;
}

.background {
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  position: fixed;
  z-index: -1;
}
</style>
