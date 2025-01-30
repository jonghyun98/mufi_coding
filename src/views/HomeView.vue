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
    let isScrolling = false
    let sections = []
    let footerElement = null
    const SCROLL_DELAY = 800

    const isAtSectionBottom = (section) => {
      const rect = section.getBoundingClientRect()
      const scrollTop = window.pageYOffset || document.documentElement.scrollTop
      const sectionBottom = rect.top + scrollTop + section.offsetHeight
      const viewportBottom = scrollTop + window.innerHeight
      
      // 섹션 하단에 도달했는지 확인 (여유값 20px)
      return Math.abs(sectionBottom - viewportBottom) < 20
    }

    const isAtSectionTop = (section) => {
      const rect = section.getBoundingClientRect()
      return Math.abs(rect.top) < 20
    }

    const handleScroll = (event) => {
      if (isScrolling) return
      
      const currentSectionEl = sections[currentSection]
      const direction = event.deltaY > 0 ? 'down' : 'up'

      // 현재 섹션의 끝에 도달했는지 확인
      if (direction === 'down' && isAtSectionBottom(currentSectionEl)) {
        if (currentSection < sections.length - 1) {
          event.preventDefault()
          currentSection++
          smoothScrollToSection(currentSection)
        }
      } 
      // 현재 섹션의 시작점에 도달했는지 확인
      else if (direction === 'up' && isAtSectionTop(currentSectionEl)) {
        if (currentSection > 0) {
          event.preventDefault()
          currentSection--
          smoothScrollToSection(currentSection)
        }
      }
    }

    const smoothScrollToSection = (index) => {
      if (isScrolling) return
      
      isScrolling = true
      sections[index].scrollIntoView({ behavior: 'smooth', block: 'start' })

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
      const touchEndY = event.changedTouches[0].clientY
      const deltaY = touchStartY - touchEndY

      if (Math.abs(deltaY) < TOUCH_THRESHOLD) return

      const currentSectionEl = sections[currentSection]
      
      if (deltaY > 0 && isAtSectionBottom(currentSectionEl)) {
        if (currentSection < sections.length - 1) {
          currentSection++
          smoothScrollToSection(currentSection)
        }
      } else if (deltaY < 0 && isAtSectionTop(currentSectionEl)) {
        if (currentSection > 0) {
          currentSection--
          smoothScrollToSection(currentSection)
        }
      }
    }

    onMounted(() => {
      sections = Array.from(document.querySelectorAll('.section'))
      footerElement = document.querySelector('footer')
      
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
    })

    onBeforeUnmount(() => {
      window.removeEventListener('wheel', handleScroll)
      window.removeEventListener('touchstart', handleTouchStart)
      window.removeEventListener('touchend', handleTouchEnd)
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
  position: relative;
}

.section {
  width: 100%;
  min-height: 100vh;
  position: relative;
  display: flex;
  flex-direction: column;
  overflow-y: auto;
  scroll-behavior: smooth;

  &:not(:first-of-type) {
    padding-top: 60px;
  }
}

@include mixins.mobile {
  .section {
    padding-top: 60px;
  }
}
</style>
