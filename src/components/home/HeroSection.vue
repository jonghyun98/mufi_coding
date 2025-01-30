<template>
  <section id="hero" class="hero">
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
              <img src="@/assets/images/frame1.png" alt="Photo Frame" />
            </div>
            <div class="element kiosk">
              <img src="@/assets/images/kiosk.png" alt="Kiosk" />
            </div>
            <div class="element students">
              <img src="@/assets/images/students.png" alt="Students" />
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
  background: linear-gradient(135deg, #1a237e 0%, #283593 100%);
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
}

.hero-content {
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
</style>
