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
        }, 300) // 애니메이션 시간 더욱 단축
      }

      handleScroll = (event) => {
        const now = Date.now()
        if (isScrolling || now - lastScrollTime < 20) return // 쓰로틀링 간격 대폭 감소

        lastScrollTime = now
        const delta = event.wheelDelta || -event.detail

        if (Math.abs(delta) > 5) { // 감도 매우 증가
          if (delta < 0 && currentSection < sections.length - 1) {
            currentSection++
            smoothScroll(sections[currentSection])
          } else if (delta > 0 && currentSection > 0) {
            currentSection--
            smoothScroll(sections[currentSection])
          }
        }
      }

      // 터치 이벤트 감도도 증가
      let touchStartY = 0

      handleTouchStart = (event) => {
        touchStartY = event.touches[0].clientY
      }

      handleTouchEnd = (event) => {
        const touchEndY = event.changedTouches[0].clientY
        const delta = touchEndY - touchStartY

        if (Math.abs(delta) > 10) { // 터치 감도 대폭 증가
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
  scroll-snap-align: start;
  scroll-snap-stop: always; // 스크롤 스냅 강화
}
</style>
