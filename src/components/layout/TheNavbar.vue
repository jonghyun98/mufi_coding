<template>
  <nav class="navbar" :class="{ 'dark': isDarkSection }">
    <div class="container">
      <div class="logo">MUFI</div>
      <div class="nav-links" :class="{ 'active': isMenuOpen }">
        <a href="#features">특징</a>
        <a href="#service">서비스</a>
        <a href="#contact" class="contact-btn">문의하기</a>
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
  mounted() {
    // 섹션 변경 이벤트 리스너
    window.addEventListener('section-change', (event) => {
      const sectionId = event.detail.sectionId
      this.isDarkSection = this.getDarkSections().includes(sectionId)
    })
  },
  beforeUnmount() {
    window.removeEventListener('section-change', this.handleSectionChange)
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    getDarkSections() {
      return ['hero', 'kiosk', 'reviews']
    }
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
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
      color: vars.$primary-color;
    }

    .nav-links {
      a {
        color: vars.$dark-color;

        &:hover {
          color: vars.$primary-color;
        }
      }
    }
  }

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo {
    font-size: 1.5rem;
    font-weight: bold;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    
    a {
      color: vars.$dark-color;
      text-decoration: none;
      transition: color 0.3s;
      word-break: keep-all;
      word-wrap: break-word;
      
      &:hover {
        color: vars.$primary-color;
      }
      
      &.contact-btn {
        background: vars.$primary-color;
        color: white;
        padding: 0.5rem 1.5rem;
        border-radius: 25px;
        
        &:hover {
          background: color.adjust(vars.$primary-color, $lightness: -10%);
        }
      }
    }
  }

  .mobile-menu-btn {
    display: none;
  }

  @include mixins.mobile {
    .nav-links {
      display: none;
      
      &.active {
        display: flex;
        flex-direction: column;
        position: absolute;
        top: 100%;
        left: 0;
        width: 100%;
        background: white;
        padding: 1rem;
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      }
    }

    .mobile-menu-btn {
      display: block;
    }
  }
}
</style>
