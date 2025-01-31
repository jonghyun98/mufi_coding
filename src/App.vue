<template>
  <div id="app">
    <router-view v-slot="{ Component }">
      <keep-alive>
        <component :is="Component" />
      </keep-alive>
    </router-view>
  </div>
</template>

<script>
export default {
  name: "App",
  mounted() {
    // 모바일 브라우저의 100vh 문제 해결
    let vh = window.innerHeight * 0.01;
    document.documentElement.style.setProperty('--vh', `${vh}px`);

    window.addEventListener('resize', () => {
      vh = window.innerHeight * 0.01;
      document.documentElement.style.setProperty('--vh', `${vh}px`);
    });
  }
}
</script>

<style lang="scss">
@use '@/assets/styles/variables' as vars;
@use '@/assets/styles/mixins' as mixins;

// 전역 스타일은 main.scss로 이동
html, body {
  margin: 0;
  padding: 0;
  overflow: hidden; // 풀페이지 스크롤을 위해 필요
  height: 100%;
}

#app {
  min-height: 100vh; /* fallback */
  min-height: calc(var(--vh, 1vh) * 100);
  width: 100%;
}
</style>
