<template>
  <section class="hero">
    <div class="hero-content">
      <h1>특별한 순간을 더욱 특별하게, 무피</h1>
      <p>네컷사진관의 새로운 기준, 무피와 함께 특별한 추억을 만들어보세요</p>
      <div class="hero-buttons">
        <button class="btn primary">서비스 알아보기</button>
        <button class="btn secondary">영상 보기</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',
  computed: {
    heroBackgroundImage() {
      // 임시 이미지 URL 사용
      return 'https://images.unsplash.com/photo-1527529482837-4698179dc6ce?auto=format&fit=crop&w=1920&q=80'
    }
  }
}
</script>

<style lang="scss" scoped>
.hero {
  min-height: 100vh;
  position: relative;
  color: white;
  text-align: center;
  display: flex;
  flex-direction: column;
  
  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: v-bind('url(heroBackgroundImage)');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    filter: brightness(0.4);
    z-index: -1;
  }
}

.hero-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0 20px;
  position: relative;
  z-index: 1;

  h1 {
    font-size: 3.5rem;
    margin-bottom: 1rem;
  }

  p {
    font-size: 1.2rem;
    margin-bottom: 2rem;
    max-width: 600px;
  }
}

.hero-buttons {
  display: flex;
  gap: 1rem;
}

.btn {
  padding: 1rem 2rem;
  border: none;
  border-radius: 25px;
  font-size: 1rem;
  cursor: pointer;
  transition: transform 0.3s;

  &:hover {
    transform: translateY(-2px);
  }

  &.primary {
    background: vars.$primary-color;
    color: white;
  }

  &.secondary {
    background: transparent;
    border: 2px solid white;
    color: white;
  }
}

@include mixins.mobile {
  .hero-content {
    h1 {
      font-size: 2rem;
    }
  }

  .hero-buttons {
    flex-direction: column;
  }
}
</style>
