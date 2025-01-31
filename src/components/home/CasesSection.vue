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

        <div class="case-item">
          <div class="case-image">
            <img :src="skkuImage" alt="성균관대학교" />
          </div>
          <h3>성균관대학교</h3>
          <p>2023 대동제에서 학생들의 뜨거운 호응</p>
          <div class="case-stats">
            <div class="stat">
              <span class="value">2,200+</span>
              <span class="label">이용자</span>
            </div>
            <div class="stat">
              <span class="value">4일</span>
              <span class="label">기간</span>
            </div>
            <div class="stat">
              <span class="value">97%</span>
              <span class="label">만족도</span>
            </div>
          </div>
        </div>

        <div class="case-item">
          <div class="case-image">
            <img :src="yonseiImage" alt="연세대학교" />
          </div>
          <h3>연세대학교</h3>
          <p>2023 축제 현장의 새로운 경험</p>
          <div class="case-stats">
            <div class="stat">
              <span class="value">1,900+</span>
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
            <img :src="khuImage" alt="경희대학교" />
          </div>
          <h3>경희대학교</h3>
          <p>2023 대동제의 혁신적인 변화</p>
          <div class="case-stats">
            <div class="stat">
              <span class="value">1,700+</span>
              <span class="label">이용자</span>
            </div>
            <div class="stat">
              <span class="value">3일</span>
              <span class="label">기간</span>
            </div>
            <div class="stat">
              <span class="value">96%</span>
              <span class="label">만족도</span>
            </div>
          </div>
        </div>
      </div>

      <div class="cases-summary">
        <div class="summary-item">
          <span class="number" ref="installCount">{{ currentInstalls }}+</span>
          <span class="text">대학교 설치</span>
        </div>
        <div class="summary-item">
          <span class="number" ref="userCount">{{ currentUsers }}+</span>
          <span class="text">누적 이용자</span>
        </div>
        <div class="summary-item">
          <span class="number" ref="satisfactionCount">{{ currentSatisfaction }}%</span>
          <span class="text">평균 만족도</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import chungbukImage from '@/assets/images/chungbuk.png'
import hufsImage from '@/assets/images/hufs.png'
import seoulTechImage from '@/assets/images/seoultech.png'
import skkuImage from '@/assets/images/skku.png'
import yonseiImage from '@/assets/images/yonsei.png'
import khuImage from '@/assets/images/khu.png'

export default {
  name: 'CasesSection',
  data() {
    return {
      chungbukImage,
      hufsImage,
      seoulTechImage,
      skkuImage,
      yonseiImage,
      khuImage,
      currentInstalls: 0,
      currentUsers: 0,
      currentSatisfaction: 0,
      targetInstalls: 30,
      targetUsers: 80000,
      targetSatisfaction: 97,
      animationStarted: false
    }
  },
  mounted() {
    // 컴포넌트가 마운트되면 애니메이션 시작
    this.$nextTick(() => {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach(entry => {
            if (entry.isIntersecting && !this.animationStarted) {
              this.animationStarted = true
              this.startCountAnimation()
            }
          })
        },
        {
          threshold: 0.5,
          rootMargin: '0px'
        }
      )

      const summary = this.$el.querySelector('.cases-summary')
      if (summary) {
        observer.observe(summary)
      }
    })
  },
  methods: {
    startCountAnimation() {
      // 설치 수 애니메이션
      this.animateNumber(0, this.targetInstalls, 2000, (value) => {
        this.currentInstalls = Math.round(value)
      })
      
      // 이용자 수 애니메이션
      this.animateNumber(0, this.targetUsers, 2000, (value) => {
        this.currentUsers = Math.round(value)
      })
      
      // 만족도 애니메이션
      this.animateNumber(0, this.targetSatisfaction, 2000, (value) => {
        this.currentSatisfaction = Math.round(value)
      })
    },
    animateNumber(start, end, duration, callback) {
      const startTime = performance.now()
      
      const updateNumber = (currentTime) => {
        const elapsed = currentTime - startTime
        const progress = Math.min(elapsed / duration, 1)
        
        // easeOutExpo 이징 함수 적용
        const easeProgress = progress === 1 ? 1 : 1 - Math.pow(2, -10 * progress)
        const currentValue = start + (end - start) * easeProgress
        
        callback(currentValue)
        
        if (progress < 1) {
          requestAnimationFrame(updateNumber)
        }
      }
      
      requestAnimationFrame(updateNumber)
    }
  }
}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/_variables' as *;
@use '@/assets/styles/_mixins' as *;

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
    color: #1F1F1F;
  }

  .section-desc {
    text-align: center;
    color: #1F1F1F;
    opacity: 0.8;
    margin-bottom: 3rem;
    font-size: 1.2rem;
  }

  .case-image {
    width: 100%;
    height: 250px;
    background: linear-gradient(135deg, #1F1F1F 0%, #232323 100%);
    margin-bottom: 1.5rem;
    overflow: hidden;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.5s ease;

      &:hover {
        transform: scale(1.08);
      }
    }
  }

  .placeholder {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 1.5rem;
    font-weight: 500;
  }
}

.cases-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  margin-bottom: 4rem;
}

.case-item {
  display: block;
  background: white;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: transform 0.3s;
  padding: 0;

  &:hover {
    transform: translateY(-5px);
  }

  h3 {
    font-size: 1.5rem;
    margin: 0 0 0.5rem 0;
    color: #1F1F1F;
    padding: 0 1.5rem;
  }

  p {
    color: #1F1F1F;
    opacity: 0.8;
    margin-bottom: 1.5rem;
    line-height: 1.6;
    padding: 0 1.5rem;
  }

  .case-stats {
    padding: 0 1.5rem 1.5rem;
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
      color: #1F1F1F;
    }

    .label {
      display: block;
      font-size: 0.9rem;
      color: #1F1F1F;
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
  background: linear-gradient(135deg, #1F1F1F 0%, #232323 100%);
  border-radius: 10px;
  color: white;

  .summary-item {
    .number {
      display: block;
      font-size: 2.5rem;
      font-weight: bold;
      margin-bottom: 0.5rem;
      transition: color 0.3s ease;
      
      &.animated {
        color: #1F1F1F;
      }
    }

    .text {
      font-size: 1.1rem;
      opacity: 0.9;
    }
  }
}

.stat .value {
  color: #1F1F1F;
}

@include mobile {
  .cases {
    padding: 60px 20px;

    .case-image {
      height: 200px;
    }
  }

  .case-item {
    h3 {
      padding: 0 1rem;
    }

    p {
      padding: 0 1rem;
    }

    .case-stats {
      padding: 0 1rem 1rem;
    }
  }

  .cases-grid {
    grid-template-columns: 1fr;
  }

  .cases-summary {
    grid-template-columns: 1fr;
    padding: 2rem 1rem;
  }
}
</style> 