<template>
  <section id="service" class="service">
    <div class="container">
      <h2>무피만의 특별한 서비스</h2>
      <div class="service-grid">
        <div class="service-card">
          <img :src="kioskImage" alt="무인 키오스크">
          <div class="service-content">
            <h3>스마트 키오스크</h3>
            <ul>
              <li>직관적인 UI/UX</li>
              <li>빠른 결제 시스템</li>
              <li>다양한 커스텀 옵션</li>
            </ul>
            <a href="#" class="learn-more">자세히 보기 →</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ServiceSection',
  data() {
    return {
      kioskImage: 'https://images.unsplash.com/photo-1612538498456-e861df91d4d0?auto=format&fit=crop&w=800&q=80'
    }
  }
}
</script>

<style lang="scss" scoped>
.service {
  background: white;
  padding: 5rem 0;

  h2 {
    text-align: center;
    color: vars.$dark-color;
    margin-bottom: 3rem;
  }
}

.service-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.service-card {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: transform 0.3s;

  &:hover {
    transform: translateY(-5px);
  }

  img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }

  .service-content {
    padding: 2rem;

    h3 {
      color: vars.$dark-color;
      margin-bottom: 1rem;
    }

    ul {
      list-style: none;
      margin: 1rem 0;
      padding: 0;

      li {
        margin: 0.5rem 0;
        color: vars.$dark-color;
        &:before {
          content: "•";
          color: vars.$primary-color;
          margin-right: 0.5rem;
        }
      }
    }

    .learn-more {
      display: inline-block;
      margin-top: 1rem;
      color: vars.$primary-color;
      text-decoration: none;
      font-weight: 500;
      transition: color 0.3s;

      &:hover {
        color: color.adjust(vars.$primary-color, $lightness: -10%);
      }
    }
  }
}

@include mixins.mobile {
  .service-grid {
    grid-template-columns: 1fr;
  }
}
</style> 