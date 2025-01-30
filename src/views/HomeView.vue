<template>
  <div class="home">
    <TheNavbar />
    <HeroSection id="hero" class="section"/>
    <FeaturesSection id="features" class="section"/>
    <ServiceSection id="service" class="section"/>
    <TheFooter />
  </div>
</template>

<script>
import { onMounted, onBeforeUnmount } from 'vue'
import HeroSection from '@/components/home/HeroSection.vue'
import FeaturesSection from '@/components/home/FeaturesSection.vue'
import ServiceSection from '@/components/home/ServiceSection.vue'
import TheNavbar from '@/components/layout/TheNavbar.vue'
import TheFooter from '@/components/layout/TheFooter.vue'

export default {
  name: 'HomeView',
  components: {
    HeroSection,
    FeaturesSection,
    ServiceSection,
    TheNavbar,
    TheFooter
  },
  setup() {
    let handleScroll, handleTouchStart, handleTouchEnd

    onMounted(() => {
      const sections = document.querySelectorAll('.section')
      let isScrolling = false
      let currentSection = 0
      let lastScrollTime = Date.now()
      
      const smoothScroll = (target) => {
        isScrolling = true
        target.scrollIntoView({
          behavior: 'smooth',
          block: 'start'
        })
        setTimeout(() => {
          isScrolling = false
        }, 500) // 애니메이션 시간 더 단축
      }

      // 스크롤 이벤트 핸들러 - 디바운스 제거하고 쓰로틀링으로 변경
      handleScroll = (event) => {
        const now = Date.now()
        if (isScrolling || now - lastScrollTime < 50) return // 쓰로틀링 간격 50ms
        
        lastScrollTime = now
        const delta = event.wheelDelta || -event.detail

        if (Math.abs(delta) > 10) { // 감도 더 증가
          if (delta < 0 && currentSection < sections.length - 1) {
            currentSection++
            smoothScroll(sections[currentSection])
          } else if (delta > 0 && currentSection > 0) {
            currentSection--
            smoothScroll(sections[currentSection])
          }
        }
      }

      // 터치 이벤트도 더 민감하게 조정
      let touchStartY = 0

      handleTouchStart = (event) => {
        touchStartY = event.touches[0].clientY
      }

      handleTouchEnd = (event) => {
        const touchEndY = event.changedTouches[0].clientY
        const delta = touchEndY - touchStartY

        if (Math.abs(delta) > 20) { // 터치 감도 더 증가
          if (delta < 0 && currentSection < sections.length - 1) {
            currentSection++
            smoothScroll(sections[currentSection])
          } else if (delta > 0 && currentSection > 0) {
            currentSection--
            smoothScroll(sections[currentSection])
          }
        }
      }

      window.addEventListener('wheel', handleScroll, { passive: false })
      window.addEventListener('touchstart', handleTouchStart, { passive: true })
      window.addEventListener('touchend', handleTouchEnd, { passive: true })
    })

    onBeforeUnmount(() => {
      if (handleScroll) window.removeEventListener('wheel', handleScroll)
      if (handleTouchStart) window.removeEventListener('touchstart', handleTouchStart)
      if (handleTouchEnd) window.removeEventListener('touchend', handleTouchEnd)
    })
  }
}
</script>

<style lang="scss" scoped>
.home {
  height: 100vh;
  overflow: hidden;
  scroll-behavior: smooth;
}

.section {
  min-height: 100vh;
  position: relative;
  overflow: hidden;
  padding-top: 60px;
  scroll-snap-align: start; // 스크롤 스냅 추가
}
</style>
