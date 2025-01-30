<template>
  <div class="home">
    <TheNavbar />
    <div class="sections-container">
      <HeroSection id="hero" class="section"/>
      <FeaturesSection id="features" class="section"/>
      <ServiceSection id="service" class="section"/>
      <KioskSection id="kiosk" class="section"/>
      <CasesSection id="cases" class="section"/>
      <ReviewsSection id="reviews" class="section"/>
      <ComparisonSection id="comparison" class="section"/>
      <FaqSection id="faq" class="section"/>
      <ContactSection id="contact" class="section"/>
    </div>
    <TheFooter />
  </div>
</template>

<script>
import { onMounted, onBeforeUnmount } from 'vue'
import HeroSection from '@/components/home/HeroSection.vue'
import FeaturesSection from '@/components/home/FeaturesSection.vue'
import ServiceSection from '@/components/home/ServiceSection.vue'
import KioskSection from '@/components/home/KioskSection.vue'
import CasesSection from '@/components/home/CasesSection.vue'
import ReviewsSection from '@/components/home/ReviewsSection.vue'
import ComparisonSection from '@/components/home/ComparisonSection.vue'
import FaqSection from '@/components/home/FaqSection.vue'
import ContactSection from '@/components/home/ContactSection.vue'
import TheNavbar from '@/components/layout/TheNavbar.vue'
import TheFooter from '@/components/layout/TheFooter.vue'

export default {
  name: 'HomeView',
  components: {
    HeroSection,
    FeaturesSection,
    ServiceSection,
    KioskSection,
    CasesSection,
    ReviewsSection,
    ComparisonSection,
    FaqSection,
    ContactSection,
    TheNavbar,
    TheFooter
  },
  setup() {
    let currentSection = 0
    let sections = []
    let isScrolling = false
    const SCROLL_DELAY = 800

    const setupIntersectionObserver = () => {
      const options = {
        root: null,
        rootMargin: '0px',
        threshold: 0.95 // 95% 이상 보일 때 감지
      }

      const sectionObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const index = sections.findIndex(section => section === entry.target)
            if (index !== -1) {
              currentSection = index
            }
          }
        })
      }, options)

      sections.forEach(section => sectionObserver.observe(section))
      return sectionObserver
    }

    const handleScroll = (event) => {
      if (isScrolling) return

      const currentSectionEl = sections[currentSection]
      if (!currentSectionEl) return

      const { scrollTop, scrollHeight, clientHeight } = currentSectionEl
      const isAtBottom = scrollHeight - scrollTop - clientHeight <= 1
      const isAtTop = scrollTop <= 0

      // 섹션 내부 스크롤이 끝에 도달했을 때만 섹션 전환
      if (event.deltaY > 0 && isAtBottom) { // 아래로 스크롤
        if (currentSection < sections.length - 1) {
          event.preventDefault()
          moveToSection(currentSection + 1)
        }
      } else if (event.deltaY < 0 && isAtTop) { // 위로 스크롤
        if (currentSection > 0) {
          event.preventDefault()
          moveToSection(currentSection - 1)
        }
      }
    }

    const moveToSection = (index) => {
      if (isScrolling || index < 0 || index >= sections.length) return

      isScrolling = true
      currentSection = index

      sections[index].scrollIntoView({
        behavior: 'smooth',
        block: 'start'
      })

      setTimeout(() => {
        isScrolling = false
      }, SCROLL_DELAY)
    }

    // 터치 이벤트 처리
    let touchStartY = 0
    const TOUCH_THRESHOLD = 50

    const handleTouchStart = (event) => {
      touchStartY = event.touches[0].clientY
    }

    const handleTouchEnd = (event) => {
      if (isScrolling) return

      const touchEndY = event.changedTouches[0].clientY
      const deltaY = touchStartY - touchEndY

      if (Math.abs(deltaY) < TOUCH_THRESHOLD) return

      const currentSectionEl = sections[currentSection]
      const { scrollTop, scrollHeight, clientHeight } = currentSectionEl
      const isAtBottom = scrollHeight - scrollTop - clientHeight <= 1
      const isAtTop = scrollTop <= 0

      if (deltaY > 0 && isAtBottom && currentSection < sections.length - 1) {
        moveToSection(currentSection + 1)
      } else if (deltaY < 0 && isAtTop && currentSection > 0) {
        moveToSection(currentSection - 1)
      }
    }

    onMounted(() => {
      sections = Array.from(document.querySelectorAll('.section'))
      const observer = setupIntersectionObserver()
      
      window.addEventListener('wheel', handleScroll, { passive: false })
      window.addEventListener('touchstart', handleTouchStart, { passive: true })
      window.addEventListener('touchend', handleTouchEnd, { passive: true })

      // 네비게이션 바 색상 변경 Observer
      const navObserver = new IntersectionObserver(
        (entries) => {
          entries.forEach(entry => {
            if (entry.isIntersecting) {
              window.dispatchEvent(new CustomEvent('section-change', {
                detail: { sectionId: entry.target.id }
              }))
            }
          })
        },
        { threshold: 0.5 }
      )

      sections.forEach(section => navObserver.observe(section))

      onBeforeUnmount(() => {
        observer.disconnect()
        navObserver.disconnect()
        window.removeEventListener('wheel', handleScroll)
        window.removeEventListener('touchstart', handleTouchStart)
        window.removeEventListener('touchend', handleTouchEnd)
      })
    })
  }
}
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  background: white;
}

.sections-container {
  width: 100%;
  height: 100vh;
  overflow-y: auto;
  scroll-behavior: smooth;
  scroll-snap-type: y mandatory;
}

.section {
  width: 100%;
  min-height: 100vh;
  position: relative;
  scroll-snap-align: start;
  scroll-snap-stop: always;
  overflow-y: auto;
  
  &:first-of-type {
    padding-top: 0;
  }

  &:last-of-type {
    margin-bottom: 60px;
  }
}

@include mixins.mobile {
  .section {
    padding-top: 60px;
  }
}
</style>
