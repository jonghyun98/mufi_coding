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
    onMounted(() => {
      const sections = document.querySelectorAll('.section')
      
      // 네비게이션 바 색상 변경 Observer만 유지
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
  }
}
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  min-height: 100%;
  background: white;
}

.sections-container {
  width: 100%;
}

.section {
  width: 100%;
  min-height: 100vh;
  position: relative;
  padding: 80px 0;

  &:first-of-type {
    padding-top: 0;
  }
}

@include mixins.mobile {
  .section {
    padding-top: 60px;
  }
}
</style>
