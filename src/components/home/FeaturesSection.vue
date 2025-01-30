<template>
  <section id="features" class="features">
    <div class="container">
      <h2>왜 무피일까요?</h2>
      <div class="features-grid">
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M12,0A12,12,0,1,0,24,12,12,12,0,0,0,12,0Zm0,22A10,10,0,1,1,22,12,10,10,0,0,1,12,22Z"/>
              <path d="M12,6a1,1,0,0,0-1,1v5H7a1,1,0,0,0,0,2h5a1,1,0,0,0,1-1V7A1,1,0,0,0,12,6Z"/>
            </svg>
          </div>
          <h3>24시간 운영</h3>
          <p>완벽한 무인화 시스템으로 언제든지 이용 가능</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M23,22H3a1,1,0,0,1-1-1V1A1,1,0,0,1,3,0H23a1,1,0,0,1,1,1V21A1,1,0,0,1,23,22ZM4,20H22V2H4Z"/>
              <path d="M19.5,9h-7a1,1,0,0,1,0-2h7a1,1,0,0,1,0,2Z"/>
              <path d="M19.5,13h-7a1,1,0,0,1,0-2h7a1,1,0,0,1,0,2Z"/>
              <path d="M19.5,17h-7a1,1,0,0,1,0-2h7a1,1,0,0,1,0,2Z"/>
              <circle cx="8.5" cy="8" r="1.5"/>
              <circle cx="8.5" cy="12" r="1.5"/>
              <circle cx="8.5" cy="16" r="1.5"/>
            </svg>
          </div>
          <h3>데이터 기반 운영</h3>
          <p>실시간 데이터 분석으로 효율적인 운영 관리</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M21,2H3A1,1,0,0,0,2,3V21a1,1,0,0,0,1,1H21a1,1,0,0,0,1-1V3A1,1,0,0,0,21,2ZM20,20H4V4H20Z"/>
              <path d="M9.5,11A1.5,1.5,0,1,0,8,9.5,1.5,1.5,0,0,0,9.5,11Z"/>
              <path d="M16,17H8a1,1,0,0,1-.89-1.45l2-4a1,1,0,0,1,1.78,0l1.11,2.22,3-6a1,1,0,0,1,1.78,0l3,6A1,1,0,0,1,19,15H16Z"/>
            </svg>
          </div>
          <h3>트렌디한 디자인</h3>
          <p>MZ세대를 위한 감각적인 프레임 디자인</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'FeaturesSection'
}
</script>

<style lang="scss" scoped>
.features {
  padding: 5rem 0;
  background: vars.$light-color;

  h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 3rem;
  }
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.feature-card {
  background: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  text-align: center;
  transition: transform 0.3s;

  &:hover {
    transform: translateY(-5px);
  }

  .feature-icon {
    width: 64px;
    height: 64px;
    margin: 0 auto 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;

    .icon {
      width: 40px;
      height: 40px;
      fill: vars.$primary-color;
    }
  }

  h3 {
    margin-bottom: 1rem;
  }
}

@include mixins.mobile {
  .features-grid {
    grid-template-columns: 1fr;
  }
}
</style> 