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
    let scrollTimeout = null

    const handleScroll = (event) => {
      event.preventDefault()
      
      if (isScrolling) return
      
      const now = Date.now()
      if (now - lastScrollTime < 1000) return

      lastScrollTime = now
      const delta = event.wheelDelta || -event.detail

      if (delta < 0 && currentSection < sections.length - 1) {
        currentSection++
        smoothScroll(sections[currentSection])
      } else if (delta > 0 && currentSection > 0) {
        currentSection--
        smoothScroll(sections[currentSection])
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
      if (isScrolling) return
      touchStartY = event.touches[0].clientY
    }

    const handleTouchEnd = (event) => {
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

      sections.forEach(section => {
        observer.observe(section)
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
  max-width: 1920px;
  margin: 0 auto;
  overflow: hidden;
  background: white;
}

.section {
  aspect-ratio: 1920/1080;
  width: 100%;
  height: 100vh;
  min-height: 1080px;
  position: relative;
  padding-top: 60px;
  scroll-snap-align: start;
  scroll-snap-stop: always;
  display: flex;
  align-items: center;
}

@media (max-width: 1920px) {
  .section {
    height: 100vh;
    min-height: auto;
    aspect-ratio: auto;
  }
}
</style>
