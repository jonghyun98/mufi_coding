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
    let lastScrollTime = 0
    let sections = []
    let touchStartY = 0
    let scrollTimeout = null
    let isLastSection = false

    const handleScroll = (event) => {
      const now = Date.now()
      if (isScrolling || now - lastScrollTime < 1000) return
      lastScrollTime = now

      // 마지막 섹션에서 위로 스크롤할 때는 이벤트 처리
      if (isLastSection && event.wheelDelta > 0) {
        event.preventDefault()
        currentSection--
        smoothScroll(sections[currentSection])
        isLastSection = false
        return
      }

      // 마지막 섹션이 아닐 때는 모든 스크롤 이벤트 처리
      if (!isLastSection) {
        event.preventDefault()
        const delta = event.wheelDelta || -event.detail

        if (delta < 0 && currentSection < sections.length - 1) {
          currentSection++
          if (currentSection === sections.length - 1) {
            isLastSection = true
          }
          smoothScroll(sections[currentSection])
        } else if (delta > 0 && currentSection > 0) {
          currentSection--
          smoothScroll(sections[currentSection])
        }
      }
    }

    const smoothScroll = (target) => {
      if (isScrolling) return
      
      isScrolling = true
      target.scrollIntoView({
        behavior: 'smooth',
        block: 'start'
      })

      clearTimeout(scrollTimeout)
      scrollTimeout = setTimeout(() => {
        isScrolling = false
      }, 1000)
    }

    const handleTouchStart = (event) => {
      if (currentSection === sections.length - 1) {
        return;
      }
      if (isScrolling) return
      touchStartY = event.touches[0].clientY
    }

    const handleTouchEnd = (event) => {
      if (currentSection === sections.length - 1) {
        return;
      }
      if (isScrolling) return
      
      const touchEndY = event.changedTouches[0].clientY
      const deltaY = touchEndY - touchStartY

      if (Math.abs(deltaY) > 50) {
        if (deltaY < 0 && currentSection < sections.length - 1) {
          currentSection++
          smoothScroll(sections[currentSection])
        } else if (deltaY > 0 && currentSection > 0) {
          currentSection--
          smoothScroll(sections[currentSection])
        }
      }
    }

    onMounted(() => {
      sections = Array.from(document.querySelectorAll('.section'))
      
      window.addEventListener('wheel', handleScroll, { passive: false })
      window.addEventListener('touchstart', handleTouchStart, { passive: true })
      window.addEventListener('touchend', handleTouchEnd, { passive: true })

      // Intersection Observer 설정 - 네비게이션 바 색상 변경용
      const navObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const sectionId = entry.target.id
            // TheNavbar 컴포넌트에 이벤트 발송
            window.dispatchEvent(new CustomEvent('section-change', {
              detail: { sectionId }
            }))
          }
        })
      }, {
        threshold: 0.6
      })

      sections.forEach(section => {
        navObserver.observe(section)
      })

      // 섹션 활성화 감지용 Observer
      const sectionObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('active')
          } else {
            entry.target.classList.remove('active')
          }
        })
      }, {
        threshold: 0.3
      })

      sections.forEach(section => {
        sectionObserver.observe(section)
      })
    })

    onBeforeUnmount(() => {
      window.removeEventListener('wheel', handleScroll)
      window.removeEventListener('touchstart', handleTouchStart)
      window.removeEventListener('touchend', handleTouchEnd)
      if (scrollTimeout) clearTimeout(scrollTimeout)
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
  min-height: 100vh;
}

.section {
  width: 100%;
  min-height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;

  &:not(:first-of-type) {
    padding-top: 60px;
  }

  &:last-of-type {
    margin-bottom: 0;
  }
}

@include mixins.mobile {
  .section {
    padding-top: 60px;
  }
}
</style>
