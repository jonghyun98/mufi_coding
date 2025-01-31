<template>
  <section id="reviews" class="reviews">
    <div class="container">
      <h2>고객 후기</h2>
      <p class="section-desc">무피와 함께한 특별한 순간들을 소개합니다</p>
      
      <div class="reviews-grid">
        <div class="review-card">
          <div class="review-header">
            <div class="reviewer-info">
              <div class="reviewer-image">
                <div class="placeholder-image">C</div>
              </div>
              <div class="reviewer-details">
                <h3>충북대학교 총학생회</h3>
                <span class="position">축제 기획단</span>
              </div>
            </div>
            <div class="rating">
              <svg viewBox="0 0 24 24" class="star" v-for="n in 5" :key="n">
                <path d="M12 17.27L18.18 21l-1.64-7.03L22 9.24l-7.19-.61L12 2 9.19 8.63 2 9.24l5.46 4.73L5.82 21z"/>
              </svg>
            </div>
          </div>
          <p class="review-text">
            "축제 기간 동안 학생들의 반응이 정말 좋았습니다. 특히 총장님과 함께 찍는 '총장네컷' 이벤트는 대학 축제의 새로운 문화를 만들어냈다고 생각합니다."
          </p>
        </div>

        <div class="review-card">
          <div class="review-header">
            <div class="reviewer-info">
              <div class="reviewer-image">
                <div class="placeholder-image">H</div>
              </div>
              <div class="reviewer-details">
                <h3>한국외대 축제준비위원회</h3>
                <span class="position">부위원장</span>
              </div>
            </div>
            <div class="rating">
              <svg viewBox="0 0 24 24" class="star" v-for="n in 5" :key="n">
                <path d="M12 17.27L18.18 21l-1.64-7.03L22 9.24l-7.19-.61L12 2 9.19 8.63 2 9.24l5.46 4.73L5.82 21z"/>
              </svg>
            </div>
          </div>
          <p class="review-text">
            "무인 키오스크라 걱정했는데, 사용이 너무 쉽고 결과물도 훌륭해서 학생들의 만족도가 매우 높았습니다. 다음 축제에도 꼭 다시 설치하고 싶습니다."
          </p>
        </div>

        <div class="review-card">
          <div class="review-header">
            <div class="reviewer-info">
              <div class="reviewer-image">
                <div class="placeholder-image">S</div>
              </div>
              <div class="reviewer-details">
                <h3>서울과기대 학생회</h3>
                <span class="position">회장</span>
              </div>
            </div>
            <div class="rating">
              <svg viewBox="0 0 24 24" class="star" v-for="n in 5" :key="n">
                <path d="M12 17.27L18.18 21l-1.64-7.03L22 9.24l-7.19-.61L12 2 9.19 8.63 2 9.24l5.46 4.73L5.82 21z"/>
              </svg>
            </div>
          </div>
          <p class="review-text">
            "실시간 데이터 분석 기능이 매우 유용했습니다. 어떤 시간대에 학생들이 많이 이용하는지 파악할 수 있어서 운영 계획 수립에 큰 도움이 되었습니다."
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '@/assets/styles/_variables' as *;
@use '@/assets/styles/_mixins' as *;

.reviews {
  background: #1F1F1F;
  padding: 5rem 0;
  color: white;

  h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 1rem;
  }

  .section-desc {
    text-align: center;
    opacity: 0.9;
    margin-bottom: 3rem;
    font-size: 1.2rem;
  }
}

.reviews-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.review-card {
  background: rgba(37, 37, 37, 0.3);
  padding: 2rem;
  border-radius: 10px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: transform 0.3s;

  &:hover {
    transform: translateY(-5px);
  }
}

.review-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.5rem;
}

.reviewer-info {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.reviewer-image {
  .placeholder-image {
    width: 50px;
    height: 50px;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5rem;
    font-weight: bold;
  }
}

.reviewer-details {
  h3 {
    font-size: 1.1rem;
    margin-bottom: 0.25rem;
  }

  .position {
    font-size: 0.9rem;
    opacity: 0.8;
  }
}

.rating {
  display: flex;
  gap: 0.25rem;

  .star {
    width: 20px;
    height: 20px;
    fill: #ffd700;
  }
}

.review-text {
  font-size: 1rem;
  line-height: 1.6;
  opacity: 0.9;
}

@include mobile {
  .reviews-grid {
    grid-template-columns: 1fr;
    padding: 0 1rem;
  }

  .review-card {
    margin-bottom: 1rem;
  }
}
</style> 