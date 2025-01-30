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
    // Intersection Observer 설정
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            // 각 섹션의 배경색에 따라 네비게이션바 스타일 변경
            const sectionId = entry.target.id;
            this.isDarkSection = this.getDarkSections().includes(sectionId);
          }
        });
      },
      {
        threshold: 0.6
      }
    );

    // 모든 섹션 관찰
    document.querySelectorAll('section[id]').forEach(section => {
      observer.observe(section);
    });
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    getDarkSections() {
      // 어두운 배경색을 가진 섹션들의 ID
      return ['hero', 'kiosk', 'reviews'];
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
