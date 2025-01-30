<template>
  <header class="header">
    <TheNavbar />
  </header>
</template>

<script>
import TheNavbar from './TheNavbar.vue'

export default {
  name: 'TheHeader',
  components: {
    TheNavbar
  }
}
</script>

<style lang="scss" scoped>
.header {
  position: fixed;
  width: 100%;
  z-index: 1000;
}
</style> 