<template>
  <nav class="navbar" :class="{ 'dark': isDarkSection }">
    <div class="container">
      <div class="logo">MUFI</div>
      <div class="nav-links" :class="{ 'active': isMenuOpen }">
        <a href="#features" @click.prevent="scrollToSection('features')">특징</a>
        <a href="#service" @click.prevent="scrollToSection('service')">서비스</a>
        <a href="#contact" @click.prevent="scrollToSection('contact')" class="contact-btn">문의하기</a>
      </div>
      <button class="mobile-menu-btn" @click="toggleMenu">
        <span></span>
      </button>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'TheNavbar',
  data() {
    return {
      isMenuOpen: false,
      isDarkSection: true
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    scrollToSection(sectionId) {
      const section = document.getElementById(sectionId)
      if (section) {
        section.scrollIntoView({ behavior: 'smooth' })
        this.isMenuOpen = false
      }
    },
    getDarkSections() {
      return ['hero', 'kiosk', 'reviews']
    }
  },
  mounted() {
    // 섹션 변경 이벤트 리스너
    window.addEventListener('section-change', (event) => {
      const sectionId = event.detail.sectionId
      this.isDarkSection = this.getDarkSections().includes(sectionId)
    })
  },
  beforeUnmount() {
    window.removeEventListener('section-change', this.handleSectionChange)
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 80px;
  z-index: 1000;
  transition: all 0.3s ease;
  background: transparent;

  &.dark {
    .logo {
      color: white;
    }

    .nav-links {
      a {
        color: white;

        &:hover {
          color: rgba(255, 255, 255, 0.8);
        }
      }
    }
  }

  &:not(.dark) {
    background: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);

    .logo {
      color: #1F1F1F;
    }

    .nav-links {
      a {
        color: #1F1F1F;

        &:hover {
          color: #232323;
        }
      }
    }
  }

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 100%;
    padding: 0 40px;
  }

  .logo {
    font-size: 1.8rem;
    font-weight: bold;
  }

  .nav-links {
    display: flex;
    gap: 3rem;
    align-items: center;
    height: 100%;
    
    a {
      color: #1F1F1F;
      text-decoration: none;
      transition: color 0.3s;
      word-break: keep-all;
      word-wrap: break-word;
      font-size: 1.1rem;
      
      &:hover {
        color: #232323;
      }
      
      &.contact-btn {
        background: #1F1F1F;
        color: white;
        padding: 0.8rem 2rem;
        border-radius: 30px;
        font-weight: 500;
        
        &:hover {
          background: #232323;
          transform: translateY(-2px);
          transition: all 0.3s ease;
        }
      }
    }
  }

  .mobile-menu-btn {
    display: none;
  }

  @include mixins.mobile {
    height: 60px;
    
    .container {
      padding: 0 20px;
    }

    .nav-links {
      &.active {
        top: 60px;
        padding: 1.5rem;
        gap: 1.5rem;
      }
    }

    .mobile-menu-btn {
      display: block;
    }
  }
}
</style>
