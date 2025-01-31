<template>
  <section id="faq" class="faq">
    <div class="container">
      <h2>자주 묻는 질문</h2>
      <p class="section-desc">무피에 대해 궁금하신 점을 확인하세요</p>

      <div class="faq-grid">
        <div class="faq-item" v-for="(faq, index) in faqs" :key="index" 
             :class="{ 'active': activeIndex === index }"
             @click="toggleFaq(index)">
          <div class="faq-header">
            <h3>{{ faq.question }}</h3>
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M16.59 8.59L12 13.17 7.41 8.59 6 10l6 6 6-6z"/>
            </svg>
          </div>
          <div class="faq-content">
            <p>{{ faq.answer }}</p>
          </div>
        </div>
      </div>

      <div class="faq-cta">
        <p>더 궁금하신 점이 있으신가요?</p>
        <button class="btn primary">1:1 문의하기</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'FaqSection',
  data() {
    return {
      activeIndex: null,
      faqs: [
        {
          question: '무피 키오스크는 어떤 방식으로 운영되나요?',
          answer: '무피 키오스크는 완전 무인 시스템으로 24시간 운영이 가능합니다. 실시간 원격 모니터링과 데이터 분석을 통해 안정적인 운영을 보장합니다.'
        },
        {
          question: '설치 및 철수는 얼마나 걸리나요?',
          answer: '숙련된 전문 설치팀이 2시간 이내로 설치를 완료합니다. 철수 역시 2시간 이내에 마무리되어 행사 운영에 차질이 없도록 합니다.'
        },
        {
          question: '커스텀 프레임 제작도 가능한가요?',
          answer: '네, 행사나 학교의 특성에 맞는 맞춤형 프레임을 무료로 제작해드립니다. 로고나 특별한 디자인 요청도 가능합니다.'
        },
        {
          question: '고장이나 문제 발생 시 어떻게 대응하나요?',
          answer: '24시간 기술 지원팀이 대기하고 있으며, 원격으로 즉시 대응이 가능합니다. 필요시 현장 출동 서비스도 제공됩니다.'
        },
        {
          question: '결제 시스템은 어떻게 되나요?',
          answer: '카드 결제와 간편 결제(카카오페이, 네이버페이 등)를 모두 지원합니다. 안전한 결제를 위해 최신 보안 시스템을 적용하고 있습니다.'
        }
      ]
    }
  },
  methods: {
    toggleFaq(index) {
      this.activeIndex = this.activeIndex === index ? null : index
    }
  }
}
</script>

<style lang="scss" scoped>
.faq {
  background: white;
  padding: 5rem 0;

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
}

.faq-grid {
  max-width: 800px;
  margin: 0 auto;
}

.faq-item {
  background: white;
  border: 1px solid rgba(0,0,0,0.1);
  border-radius: 10px;
  margin-bottom: 1rem;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.3s ease;

  &:hover {
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }

  &.active {
    .faq-header {
      background: linear-gradient(135deg, #1F1F1F 0%, #252525 100%);
      color: white;

      .icon {
        transform: rotate(180deg);
        fill: white;
      }
    }

    .faq-content {
      max-height: 300px;
      padding: 1.5rem;
    }
  }
}

.faq-header {
  padding: 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s ease;

  h3 {
    font-size: 1.1rem;
    margin: 0;
    font-weight: 500;
  }

  .icon {
    width: 24px;
    height: 24px;
    transition: transform 0.3s ease;
    fill: #1F1F1F;
  }
}

.faq-content {
  max-height: 0;
  padding: 0 1.5rem;
  overflow: hidden;
  transition: all 0.3s ease;
  background: rgba(0,0,0,0.02);

  p {
    margin: 0;
    color: #1F1F1F;
    line-height: 1.6;
  }
}

.faq-cta {
  text-align: center;
  margin-top: 3rem;

  p {
    margin-bottom: 1rem;
    color: #1F1F1F;
  }

  .btn.primary {
    padding: 1rem 2rem;
    font-size: 1.1rem;
    background: #1F1F1F;
    color: white;
    border: none;
    border-radius: 25px;
    cursor: pointer;
    transition: transform 0.3s;

    &:hover {
      transform: translateY(-2px);
    }
  }
}

@include mixins.mobile {
  .faq-grid {
    margin: 0 1rem;
  }

  .faq-header h3 {
    font-size: 1rem;
    padding-right: 1rem;
  }
}
</style> 