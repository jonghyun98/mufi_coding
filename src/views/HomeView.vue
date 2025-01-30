<template>
  <div class="home">
    <TheNavbar />
    <HeroSection id="hero" class="section"/>
    <FeaturesSection id="features" class="section"/>
    <ServiceSection id="service" class="section"/>
    <KioskSection id="kiosk" class="section"/>
    <CasesSection id="cases" class="section"/>
    <ReviewsSection id="reviews" class="section"/>
    <ComparisonSection id="comparison" class="section"/>
    <FaqSection id="faq" class="section"/>
    <ContactSection id="contact" class="section"/>
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

    const handleScroll = (event) => {
      const now = Date.now()
      if (isScrolling || now - lastScrollTime < 800) return

      lastScrollTime = now
      const delta = event.wheelDelta || -event.detail

      if (Math.abs(delta) > 30) {
        if (delta < 0 && currentSection < sections.length - 1) {
          currentSection++
          smoothScroll(sections[currentSection])
        } else if (delta > 0 && currentSection > 0) {
          currentSection--
          smoothScroll(sections[currentSection])
        }
      }
    }

    const smoothScroll = (target) => {
      isScrolling = true
      target.scrollIntoView({
        behavior: 'smooth',
        block: 'start'
      })
      setTimeout(() => {
        isScrolling = false
      }, 800)
    }

    const handleTouchStart = (event) => {
      touchStartY = event.touches[0].clientY
    }

    const handleTouchEnd = (event) => {
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
      
      // Intersection Observer 설정
      const observer = new IntersectionObserver((entries) => {
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

      // 모든 섹션에 observer 적용
      sections.forEach(section => {
        observer.observe(section)
      })

      window.addEventListener('wheel', handleScroll)
      window.addEventListener('touchstart', handleTouchStart)
      window.addEventListener('touchend', handleTouchEnd)
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
  scroll-snap-stop: always;
}
</style>
