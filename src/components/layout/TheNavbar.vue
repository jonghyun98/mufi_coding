<template>
  <nav class="navbar">
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
      isMenuOpen: false
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    }
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: rgba(255, 255, 255, 0.95);
  z-index: 1000;
  padding: 1rem 0;

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: vars.$primary-color;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    
    a {
      color: vars.$dark-color;
      text-decoration: none;
      transition: color 0.3s;
      
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
