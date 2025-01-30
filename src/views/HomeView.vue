<template>
  <div class="home">
    <TheNavbar />
    <HeroSection id="hero"/>
    <FeaturesSection id="features"/>
    <ServiceSection id="service"/>
    <KioskSection id="kiosk"/>
    <CasesSection id="cases"/>
    <ReviewsSection id="reviews"/>
    <ComparisonSection id="comparison"/>
    <FaqSection id="faq"/>
    <ContactSection id="contact"/>
    <TheFooter />
  </div>
</template>

<script>
import { onMounted } from 'vue'
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
    onMounted(() => {
      // Intersection Observer 설정만 유지
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
      document.querySelectorAll('section').forEach(section => {
        observer.observe(section)
      })
    })
  }
}
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  min-height: 100%;
  background: white;
}

section {
  min-height: 100vh;
  position: relative;
  padding-top: 60px;
  width: 100%;
}
</style>
