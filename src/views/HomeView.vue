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
    let lastScrollTime = Date.now()
    let sections = []
    let footerElement = null
    const SCROLL_DELAY = 800

    const isElementInViewport = (el) => {
      const rect = el.getBoundingClientRect()
      return (
        rect.top <= 0 && 
        rect.bottom >= 0
      )
    }

    const canScrollToNextSection = (currentSection) => {
      const section = sections[currentSection]
      if (!section) return false
      
      const sectionHeight = section.scrollHeight
      const viewportHeight = window.innerHeight
      const scrollTop = section.getBoundingClientRect().top
      const scrolled = Math.abs(scrollTop)
      
      return scrolled >= (sectionHeight - viewportHeight)
    }

    const handleScroll = (event) => {
      const now = Date.now()
      if (isScrolling || now - lastScrollTime < SCROLL_DELAY) return
      
      const direction = event.wheelDelta > 0 ? 'up' : 'down'
      const currentSectionEl = sections[currentSection]

      // 현재 섹션이 뷰포트에 있고, 아직 섹션 끝까지 스크롤하지 않았다면
      if (isElementInViewport(currentSectionEl) && !canScrollToNextSection(currentSection)) {
        // 기본 스크롤 허용
        return
      }

      // 이 시점에서는 섹션 전환이 필요하므로 기본 스크롤 방지
      event.preventDefault()
      
      if (direction === 'down' && currentSection < sections.length - 1) {
        if (canScrollToNextSection(currentSection)) {
          currentSection++
          smoothScroll(sections[currentSection])
        }
      } else if (direction === 'up' && currentSection > 0) {
        currentSection--
        smoothScroll(sections[currentSection])
      }

      lastScrollTime = now
    }

    const smoothScroll = (target) => {
      if (!target || isScrolling) return
      
      isScrolling = true
      target.scrollIntoView({ behavior: 'smooth', block: 'start' })

      setTimeout(() => {
        isScrolling = false
      }, SCROLL_DELAY)
    }

    // 터치 이벤트 처리 개선
    let touchStartY = 0
    const TOUCH_THRESHOLD = 50

    const handleTouchStart = (event) => {
      if (isScrolling) return
      touchStartY = event.touches[0].clientY
    }

    const handleTouchEnd = (event) => {
      if (isScrolling) return
      
      const touchEndY = event.changedTouches[0].clientY
      const deltaY = touchEndY - touchStartY

      if (Math.abs(deltaY) < TOUCH_THRESHOLD) return

      const direction = deltaY > 0 ? 'up' : 'down'
      handleScrollDirection(direction)
    }

    const handleScrollDirection = (direction) => {
      if (isFooterVisible() && direction === 'up') {
        currentSection = sections.length - 1
        smoothScroll(sections[currentSection])
        isLastSection = true
        return
      }

      if (direction === 'down' && currentSection < sections.length - 1) {
        currentSection++
        smoothScroll(sections[currentSection])
      } else if (direction === 'up' && currentSection > 0) {
        currentSection--
        smoothScroll(sections[currentSection])
      }
    }

    onMounted(() => {
      sections = Array.from(document.querySelectorAll('.section'))
      footerElement = document.querySelector('footer')
      
      window.addEventListener('wheel', handleScroll, { passive: false })
      window.addEventListener('touchstart', handleTouchStart, { passive: true })
      window.addEventListener('touchend', handleTouchEnd, { passive: true })

      // Intersection Observer 설정
      const observerOptions = {
        threshold: 0.5,
        rootMargin: '-10% 0px'
      }

      const navObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            window.dispatchEvent(new CustomEvent('section-change', {
              detail: { sectionId: entry.target.id }
            }))
          }
        })
      }, observerOptions)

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
  align-items: flex-start;
  justify-content: center;
  overflow-y: auto;
  overflow-x: hidden;
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
