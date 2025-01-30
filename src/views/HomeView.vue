<template>
  <div id="app">
    <TheHeader />
    <div class="fullpage-container">
      <section class="fullpage-section" id="home">
        <HeroSection />
      </section>
      <section class="fullpage-section" id="features">
        <FeaturesSection />
      </section>
      <section class="fullpage-section" id="services">
        <ServiceSection />
      </section>
      <section class="fullpage-section" id="contact">
        <ContactSection />
      </section>
      <footer class="fullpage-section" id="footer">
        <TheFooter />
      </footer>
    </div>
    <nav class="section-nav">
      <ul>
        <li v-for="(section, index) in sections" :key="section.id">
          <button 
            :class="{ active: currentSection === index }"
            @click="scrollToSection(section.id)"
          ></button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import TheHeader from '@/components/layout/TheHeader.vue'
import HeroSection from "@/components/home/HeroSection.vue"
import FeaturesSection from "@/components/home/FeaturesSection.vue"
import ServiceSection from "@/components/home/ServiceSection.vue"
import ContactSection from "@/components/home/ContactSection.vue"
import TheFooter from "@/components/layout/TheFooter.vue"

export default {
  name: "HomeView",
  components: {
    TheHeader,
    HeroSection,
    FeaturesSection,
    ServiceSection,
    ContactSection,
    TheFooter
  },
  data() {
    return {
      sections: [
        { id: 'home', name: '홈' },
        { id: 'features', name: '특징' },
        { id: 'services', name: '서비스' },
        { id: 'contact', name: '문의하기' },
        { id: 'footer', name: '푸터' }
      ],
      currentSection: 0,
      isScrolling: false
    }
  },
  mounted() {
    this.setupIntersectionObserver()
    window.addEventListener('wheel', this.handleWheel, { passive: false })
  },
  beforeUnmount() {
    window.removeEventListener('wheel', this.handleWheel)
  },
  methods: {
    setupIntersectionObserver() {
      const options = {
        root: null,
        threshold: 0.5
      }

      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const index = this.sections.findIndex(section => section.id === entry.target.id)
            if (index !== -1) {
              this.currentSection = index
            }
          }
        })
      }, options)

      this.sections.forEach(section => {
        const element = document.getElementById(section.id)
        if (element) observer.observe(element)
      })
    },
    handleWheel(e) {
      if (this.isScrolling) return
      e.preventDefault()

      this.isScrolling = true
      const direction = e.deltaY > 0 ? 1 : -1
      const nextSection = this.currentSection + direction

      if (nextSection >= 0 && nextSection < this.sections.length) {
        this.scrollToSection(this.sections[nextSection].id)
        this.currentSection = nextSection
      }

      setTimeout(() => {
        this.isScrolling = false
      }, 1000)
    },
    scrollToSection(id) {
      const element = document.getElementById(id)
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' })
      }
    }
  }
}
</script>

<style lang="scss">
.fullpage-container {
  height: 100vh;
  overflow-y: auto;
  scroll-snap-type: y mandatory;
  scroll-behavior: smooth;
}

.fullpage-section {
  height: 100vh;
  scroll-snap-align: start;
  position: relative;
}

.section-nav {
  position: fixed;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 100;

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  li {
    margin: 10px 0;
  }

  button {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    border: 2px solid vars.$primary-color;
    background: transparent;
    cursor: pointer;
    padding: 0;
    transition: all 0.3s ease;

    &.active {
      background: vars.$primary-color;
      transform: scale(1.2);
    }
  }
}

@include mixins.mobile {
  .fullpage-section {
    height: auto;
    min-height: 100vh;
  }

  .section-nav {
    display: none;
  }
}
</style>
