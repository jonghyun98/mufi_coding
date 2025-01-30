<template>
  <section id="hero" class="hero">
    <div class="hero-background"></div>
    <div class="hero-content">
      <div class="hero-text">
        <h1 class="fade-in-up">특별한 순간을 더욱 특별하게</h1>
        <p class="fade-in-up delay-1">무피와 함께하는 새로운 포토부스 경험</p>
        <div class="hero-buttons fade-in-up delay-2">
          <button class="btn primary">지금 시작하기</button>
          <button class="btn secondary">더 알아보기</button>
        </div>
      </div>
      <div class="hero-image fade-in-up delay-1">
        <div class="image-container">
          <div class="image-overlay"></div>
          <div class="floating-elements">
            <div class="element photo-frame">
              <div class="placeholder">
                <svg viewBox="0 0 24 24" class="icon">
                  <path d="M21 3H3C2 3 1 4 1 5v14c0 1.1.9 2 2 2h18c1 0 2-1 2-2V5c0-1-1-2-2-2zm0 15.92c-.02.03-.06.06-.08.08H3V5.08L3.08 5h17.83c.03.02.06.06.08.08v13.84zm-10-3.41L8.5 12.5 5 17h14l-4.5-6-3.5 4.51z"/>
                  <path d="M8.5 11a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3z"/>
                </svg>
              </div>
            </div>
            <div class="element kiosk">
              <div class="placeholder">
                <svg viewBox="0 0 24 24" class="icon">
                  <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 14H4V6h16v12z"/>
                  <path d="M6 8h12v2H6zm0 4h12v2H6zm0 4h8v2H6z"/>
                  <path d="M18 16h2v2h-2z"/>
                </svg>
              </div>
            </div>
            <div class="element students">
              <div class="placeholder">
                <svg viewBox="0 0 24 24" class="icon">
                  <path d="M16 11c1.66 0 2.99-1.34 2.99-3S17.66 5 16 5s-3 1.34-3 3 1.34 3 3 3zm-8 0c1.66 0 2.99-1.34 2.99-3S9.66 5 8 5 5 6.34 5 8s1.34 3 3 3zm0 2c-2.33 0-7 1.17-7 3.5V19h14v-2.5c0-2.33-4.67-3.5-7-3.5z"/>
                </svg>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection'
}
</script>

<style lang="scss" scoped>
.hero {
  min-height: 100vh;
  width: 100%;
  position: relative;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url('https://images.unsplash.com/photo-1517457373958-b7bdd4587205?auto=format&fit=crop&q=80');
  background-size: cover;
  background-position: center;
  filter: brightness(0.5);
  z-index: 0;

  &::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(
      135deg, 
      rgba(26, 35, 126, 0.7) 0%,
      rgba(40, 53, 147, 0.7) 100%
    );
  }
}

.hero-content {
  position: relative;
  z-index: 1;
  @include mixins.container;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  padding: 2rem;
}

.hero-text {
  color: white;
  z-index: 2;

  h1 {
    font-size: 3.5rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
    line-height: 1.2;
  }

  p {
    font-size: 1.5rem;
    opacity: 0.9;
    margin-bottom: 2rem;
  }
}

.hero-buttons {
  display: flex;
  gap: 1rem;

  .btn {
    padding: 1rem 2rem;
    font-size: 1.1rem;
    border-radius: 50px;
    border: none;
    cursor: pointer;
    transition: transform 0.3s;

    &:hover {
      transform: translateY(-2px);
    }

    &.primary {
      background: white;
      color: vars.$primary-color;
    }

    &.secondary {
      background: transparent;
      border: 2px solid white;
      color: white;
    }
  }
}

.hero-image {
  position: relative;
  z-index: 1;

  .image-container {
    position: relative;
    width: 100%;
    height: 600px;
    
    .image-overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 20px;
    }

    .floating-elements {
      position: absolute;
      width: 100%;
      height: 100%;

      .element {
        position: absolute;
        transition: transform 0.3s ease;

        img {
          width: 100%;
          height: 100%;
          object-fit: contain;
        }

        &.photo-frame {
          width: 300px;
          top: 10%;
          right: 10%;
          transform: rotate(10deg);
          animation: float 6s ease-in-out infinite;
        }

        &.kiosk {
          width: 200px;
          bottom: 20%;
          left: 10%;
          animation: float 8s ease-in-out infinite;
        }

        &.students {
          width: 350px;
          bottom: 10%;
          right: 15%;
          animation: float 7s ease-in-out infinite;
        }
      }
    }
  }
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

@include mixins.mobile {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
    padding: 2rem 1rem;
  }

  .hero-text {
    h1 {
      font-size: 2.5rem;
    }

    p {
      font-size: 1.2rem;
    }
  }

  .hero-buttons {
    justify-content: center;
    flex-direction: column;
  }

  .hero-image {
    display: none;
  }
}

.placeholder {
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  border-radius: 10px;
  backdrop-filter: blur(5px);

  .icon {
    width: 60%;
    height: 60%;
    fill: white;
    opacity: 0.9;
    filter: drop-shadow(0 2px 4px rgba(0,0,0,0.2));
  }
}

.element {
  &.photo-frame .icon {
    transform: rotate(-10deg);
  }
  
  &.kiosk .icon {
    transform: rotate(5deg);
  }
  
  &.students .icon {
    transform: rotate(-5deg);
  }
}
</style>
