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
    let isLastSection = false
    const SCROLL_DELAY = 800 // 스크롤 딜레이 시간

    const checkScrollDirection = (event) => {
      return event.wheelDelta > 0 ? 'up' : 'down'
    }

    const isFooterVisible = () => {
      if (!footerElement) return false
      const rect = footerElement.getBoundingClientRect()
      return rect.top <= window.innerHeight
    }

    const handleScroll = (event) => {
      event.preventDefault()
      
      const now = Date.now()
      if (isScrolling || now - lastScrollTime < SCROLL_DELAY) return
      
      const direction = checkScrollDirection(event)
      const isAtFooter = isFooterVisible()

      // 푸터에서의 스크롤 처리
      if (isAtFooter && direction === 'up') {
        currentSection = sections.length - 1
        smoothScroll(sections[currentSection])
        isLastSection = true
        return
      }

      // 마지막 섹션에서의 스크롤 처리
      if (isLastSection) {
        if (direction === 'up') {
          currentSection--
          smoothScroll(sections[currentSection])
          isLastSection = false
        } else if (!isAtFooter) {
          footerElement?.scrollIntoView({ behavior: 'smooth' })
        }
        return
      }

      // 일반 섹션 스크롤 처리
      if (direction === 'down' && currentSection < sections.length - 1) {
        currentSection++
        if (currentSection === sections.length - 1) {
          isLastSection = true
        }
        smoothScroll(sections[currentSection])
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
  align-items: center;
  justify-content: center;
  overflow: hidden;

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
