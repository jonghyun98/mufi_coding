<template>
  <section id="features" class="features">
    <div class="container">
      <h2>왜 무피일까요?</h2>
      <div class="features-grid">
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M12 2C6.486 2 2 6.486 2 12s4.486 10 10 10 10-4.486 10-10S17.514 2 12 2zm0 18c-4.411 0-8-3.589-8-8s3.589-8 8-8 8 3.589 8 8-3.589 8-8 8z"/>
              <path d="M13 7h-2v5.414l3.293 3.293 1.414-1.414L13 11.586z"/>
            </svg>
          </div>
          <h3>24시간 운영</h3>
          <p>완벽한 무인화 시스템으로 언제든지 이용 가능</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M20 2H4c-1.103 0-2 .897-2 2v12c0 1.103.897 2 2 2h3v3.767L13.277 18H20c1.103 0 2-.897 2-2V4c0-1.103-.897-2-2-2zm0 14h-7.277L9 18.233V16H4V4h16v12z"/>
              <path d="M7 7h10v2H7zm0 4h7v2H7z"/>
            </svg>
          </div>
          <h3>데이터 기반 운영</h3>
          <p>실시간 데이터 분석으로 효율적인 운영 관리</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M20 3H4c-1.103 0-2 .897-2 2v14c0 1.103.897 2 2 2h16c1.103 0 2-.897 2-2V5c0-1.103-.897-2-2-2zM4 19V5h16l.002 14H4z"/>
              <path d="M9.293 6.293L5.586 10l3.707 3.707 1.414-1.414L8.414 10l2.293-2.293zm5.414 0l-1.414 1.414L15.586 10l-2.293 2.293 1.414 1.414L18.414 10z"/>
            </svg>
          </div>
          <h3>트렌디한 디자인</h3>
          <p>MZ세대를 위한 감각적인 프레임 디자인</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M21 10c0-3.87-3.13-7-7-7s-7 3.13-7 7c0 3.47 2.52 6.34 5.83 6.89V20H6v2h12v-2h-3.17v-3.11C18.48 16.34 21 13.47 21 10zm-7 5c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5z"/>
            </svg>
          </div>
          <h3>대학 축제 전문</h3>
          <p>다년간의 대학 축제 운영 노하우로 완벽한 행사 진행</p>
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
  background: linear-gradient(135deg, #1F1F1F 0%, #2A2A2A 100%);
  color: white;

  h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 3rem;
    word-break: keep-all;
    word-wrap: break-word;
    color: white;
  }
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
}

.feature-card {
  background: rgba(255, 255, 255, 0.1);
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  text-align: center;
  transition: transform 0.3s;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);

  &:hover {
    transform: translateY(-5px);
    background: rgba(255, 255, 255, 0.15);
  }

  .feature-icon {
    width: 64px;
    height: 64px;
    margin: 0 auto 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 50%;
    padding: 1rem;

    .icon {
      width: 32px;
      height: 32px;
      fill: white;
    }
  }

  h3 {
    margin-bottom: 1rem;
    word-break: keep-all;
    word-wrap: break-word;
    color: white;
    font-size: 1.5rem;
  }

  p {
    word-break: keep-all;
    word-wrap: break-word;
    color: rgba(255, 255, 255, 0.9);
    line-height: 1.6;
  }
}

@include mixins.mobile {
  .features-grid {
    grid-template-columns: 1fr;
  }

  .feature-card {
    margin: 0 1rem;
  }
}
</style> 