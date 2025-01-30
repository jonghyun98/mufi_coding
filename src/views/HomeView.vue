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
      
      // Intersection Observer 설정
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach(entry => {
            // 섹션이 화면에 진입할 때만 애니메이션 적용
            if (entry.isIntersecting) {
              entry.target.classList.add('visible')
              // 네비게이션 바 색상 변경
              window.dispatchEvent(new CustomEvent('section-change', {
                detail: { sectionId: entry.target.id }
              }))
            } else {
              // 섹션이 화면에서 벗어나면 클래스 제거
              entry.target.classList.remove('visible')
            }
          })
        },
        {
          threshold: 0.2, // 20% 이상 보일 때
          rootMargin: '-10% 0px' // 상하 여백 조정
        }
      )

      sections.forEach(section => observer.observe(section))
    })
  }
}
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
  background: white;
  overflow-y: visible;
}

.sections-container {
  width: 100%;
  height: auto;
  overflow: visible;
}

.section {
  width: 100%;
  min-height: 100vh;
  position: relative;
  padding: 80px 0;
  overflow: visible;

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
