<template>
  <section id="cases" class="cases section">
    <div class="container">
      <h2 class="section-title">설치 사례</h2>
      <p class="section-desc">전국의 다양한 대학교와 행사장에서 무피를 만나보세요</p>
      <div class="cases-grid">
        <div class="case-item">
          <div class="case-image">
            <img :src="chungbukImage" alt="충북대학교" />
          </div>
          <h3>충북대학교</h3>
          <p>2023 대동제 축제 기간 동안 3일간 1,500명 이상 이용</p>
          <div class="case-stats">
            <div class="stat">
              <span class="value">1,500+</span>
              <span class="label">이용자</span>
            </div>
            <div class="stat">
              <span class="value">3일</span>
              <span class="label">기간</span>
            </div>
            <div class="stat">
              <span class="value">98%</span>
              <span class="label">만족도</span>
            </div>
          </div>
        </div>

        <div class="case-item">
          <div class="case-image">
            <img :src="hufsImage" alt="한국외국어대학교" />
          </div>
          <h3>한국외국어대학교</h3>
          <p>2023 축제 현장에서 2,000명 이상의 학생들과 함께</p>
          <div class="case-stats">
            <div class="stat">
              <span class="value">2,000+</span>
              <span class="label">이용자</span>
            </div>
            <div class="stat">
              <span class="value">4일</span>
              <span class="label">기간</span>
            </div>
            <div class="stat">
              <span class="value">96%</span>
              <span class="label">만족도</span>
            </div>
          </div>
        </div>

        <div class="case-item">
          <div class="case-image">
            <img :src="seoulTechImage" alt="서울과학기술대학교" />
          </div>
          <h3>서울과학기술대학교</h3>
          <p>2023 대동제에서 총장님과 함께한 특별한 순간</p>
          <div class="case-stats">
            <div class="stat">
              <span class="value">1,800+</span>
              <span class="label">이용자</span>
            </div>
            <div class="stat">
              <span class="value">3일</span>
              <span class="label">기간</span>
            </div>
            <div class="stat">
              <span class="value">95%</span>
              <span class="label">만족도</span>
            </div>
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

<script>
import chungbukImage from '../assets/images/chungbuk.jpg'
import hufsImage from '../assets/images/hufs.jpg'
import seoulTechImage from '../assets/images/seoultech.jpg'

export default {
  name: 'CasesSection',
  data() {
    return {
      chungbukImage,
      hufsImage,
      seoulTechImage
    }
  }
}
</script>

<style lang="scss" scoped>
.cases {
  width: 100%;
  padding: 80px 0;
  background: white;
  min-height: 100%;

  .container {
    height: auto;
    min-height: 100%;
    padding-bottom: 80px;
  }

  h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: vars.$dark-color;
  }

  .section-desc {
    text-align: center;
    color: vars.$dark-color;
    opacity: 0.8;
    margin-bottom: 3rem;
    font-size: 1.2rem;
  }

  .case-image {
    width: 100%;
    height: 250px;
    background: linear-gradient(135deg, #1a237e 0%, #283593 100%);
    border-radius: 15px;
    margin-bottom: 1.5rem;
    overflow: hidden;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);

    .placeholder {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 1.5rem;
      font-weight: 500;
      transition: transform 0.5s ease;

      &:hover {
        transform: scale(1.08);
      }
    }
  }
}

.cases-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.case-item {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: transform 0.3s;
  padding: 1.5rem;

  &:hover {
    transform: translateY(-5px);
  }

  .case-content {
    h3 {
      font-size: 1.5rem;
      margin: 1rem 0;
      color: vars.$dark-color;
    }

    p {
      color: vars.$dark-color;
      opacity: 0.8;
      margin-bottom: 1.5rem;
      line-height: 1.6;
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

  .stat {
    .value {
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
  .cases {
    padding: 60px 20px;

    .case-image {
      height: 200px;
    }
  }

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