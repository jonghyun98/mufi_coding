<template>
  <section id="cases" class="cases">
    <div class="container">
      <h2>설치 사례</h2>
      <p class="section-desc">전국의 다양한 대학교와 행사장에서 무피를 만나보세요</p>
      <div class="cases-grid">
        <div class="case-card">
          <div class="case-image">
            <div class="placeholder-image">
              <span>충북대학교</span>
            </div>
          </div>
          <div class="case-content">
            <h3>충북대학교</h3>
            <p>2023 대동제 축제 기간 동안 3일간 1,500명 이상 이용</p>
            <ul class="case-stats">
              <li>
                <span class="stat">1,500+</span>
                <span class="label">이용자 수</span>
              </li>
              <li>
                <span class="stat">3일</span>
                <span class="label">설치 기간</span>
              </li>
              <li>
                <span class="stat">98%</span>
                <span class="label">만족도</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="case-card">
          <div class="case-image">
            <div class="placeholder-image">
              <span>한국외국어대학교</span>
            </div>
          </div>
          <div class="case-content">
            <h3>한국외국어대학교</h3>
            <p>2023 축제 현장에서 2,000명 이상의 학생들과 함께</p>
            <ul class="case-stats">
              <li>
                <span class="stat">2,000+</span>
                <span class="label">이용자 수</span>
              </li>
              <li>
                <span class="stat">4일</span>
                <span class="label">설치 기간</span>
              </li>
              <li>
                <span class="stat">96%</span>
                <span class="label">만족도</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="case-card">
          <div class="case-image">
            <div class="placeholder-image">
              <span>서울과학기술대학교</span>
            </div>
          </div>
          <div class="case-content">
            <h3>서울과학기술대학교</h3>
            <p>2023 대동제에서 총장님과 함께한 특별한 순간</p>
            <ul class="case-stats">
              <li>
                <span class="stat">1,800+</span>
                <span class="label">이용자 수</span>
              </li>
              <li>
                <span class="stat">3일</span>
                <span class="label">설치 기간</span>
              </li>
              <li>
                <span class="stat">95%</span>
                <span class="label">만족도</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <div class="cases-summary">
        <div class="summary-item">
          <span class="number">20+</span>
          <span class="text">대학교 설치</span>
        </div>
        <div class="summary-item">
          <span class="number">50,000+</span>
          <span class="text">누적 이용자</span>
        </div>
        <div class="summary-item">
          <span class="number">96%</span>
          <span class="text">평균 만족도</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.cases {
  background: white;
  padding: 5rem 0;

  h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 3rem;
    color: vars.$dark-color;
  }
}

.cases-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.case-card {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: transform 0.3s;

  &:hover {
    transform: translateY(-5px);
  }

  .case-image {
    .placeholder-image {
      width: 100%;
      height: 200px;
      background: linear-gradient(135deg, #1a237e 0%, #283593 100%);
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 1.5rem;
    }
  }

  .case-content {
    padding: 2rem;

    h3 {
      font-size: 1.5rem;
      margin-bottom: 1rem;
      color: vars.$dark-color;
    }

    p {
      color: vars.$dark-color;
      margin-bottom: 1.5rem;
      opacity: 0.8;
    }
  }
}

.case-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  list-style: none;
  padding: 0;
  margin: 0;
  text-align: center;

  li {
    .stat {
      display: block;
      font-size: 1.5rem;
      font-weight: bold;
      color: vars.$primary-color;
    }

    .label {
      display: block;
      font-size: 0.9rem;
      color: vars.$dark-color;
      opacity: 0.8;
    }
  }
}

.section-desc {
  text-align: center;
  color: vars.$dark-color;
  opacity: 0.8;
  margin-bottom: 3rem;
  font-size: 1.2rem;
}

.cases-summary {
  margin-top: 4rem;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  text-align: center;
  padding: 3rem;
  background: linear-gradient(135deg, #1a237e 0%, #283593 100%);
  border-radius: 10px;
  color: white;

  .summary-item {
    .number {
      display: block;
      font-size: 2.5rem;
      font-weight: bold;
      margin-bottom: 0.5rem;
    }

    .text {
      font-size: 1.1rem;
      opacity: 0.9;
    }
  }
}

@include mixins.mobile {
  .cases-grid {
    grid-template-columns: 1fr;
    padding: 0 1rem;
  }

  .cases-summary {
    grid-template-columns: 1fr;
    padding: 2rem 1rem;
  }
}
</style> 