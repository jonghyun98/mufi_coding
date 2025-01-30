<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "App"
}
</script>

<style lang="scss">
// 전역 스타일은 main.scss로 이동
html, body {
  margin: 0;
  padding: 0;
  overflow: hidden; // 풀페이지 스크롤을 위해 필요
}
</style>
