<template>
  <section id="comparison" class="comparison">
    <div class="container">
      <h2>왜 무피여야 할까요?</h2>
      <p class="section-desc">무피만의 차별화된 경쟁력을 확인하세요</p>

      <div class="comparison-table">
        <div class="table-header">
          <div class="header-cell empty"></div>
          <div class="header-cell mufi">
            <div class="logo">MUFI</div>
            <div class="tag">네컷사진관의 새로운 기준</div>
          </div>
          <div class="header-cell others">일반 네컷사진관</div>
        </div>

        <div class="table-row">
          <div class="feature-name">데이터 분석</div>
          <div class="mufi-cell">
            <svg viewBox="0 0 24 24" class="icon check">
              <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/>
            </svg>
            실시간 데이터 분석 및 리포트 제공
          </div>
          <div class="others-cell">
            <svg viewBox="0 0 24 24" class="icon cross">
              <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"/>
            </svg>
            제공되지 않음
          </div>
        </div>

        <div class="table-row">
          <div class="feature-name">커스텀 프레임</div>
          <div class="mufi-cell">
            <svg viewBox="0 0 24 24" class="icon check">
              <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/>
            </svg>
            행사별 맞춤 프레임 무료 제작
          </div>
          <div class="others-cell">
            <svg viewBox="0 0 24 24" class="icon cross">
              <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"/>
            </svg>
            기본 프레임만 제공
          </div>
        </div>

        <div class="table-row">
          <div class="feature-name">운영 시간</div>
          <div class="mufi-cell">
            <svg viewBox="0 0 24 24" class="icon check">
              <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/>
            </svg>
            24시간 무인 운영 가능
          </div>
          <div class="others-cell">
            <svg viewBox="0 0 24 24" class="icon cross">
              <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"/>
            </svg>
            제한된 운영 시간
          </div>
        </div>

        <div class="table-row">
          <div class="feature-name">관리 시스템</div>
          <div class="mufi-cell">
            <svg viewBox="0 0 24 24" class="icon check">
              <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/>
            </svg>
            실시간 원격 모니터링 및 관리
          </div>
          <div class="others-cell">
            <svg viewBox="0 0 24 24" class="icon cross">
              <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"/>
            </svg>
            현장 관리 필요
          </div>
        </div>
      </div>

      <div class="comparison-cta">
        <button class="btn primary">지금 바로 문의하기</button>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '@/assets/styles/_variables' as *;
@use '@/assets/styles/_mixins' as *;

.comparison {
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

.comparison-table {
  max-width: 900px;
  margin: 0 auto;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.table-header {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr;
  background: linear-gradient(135deg, #1F1F1F 0%, #232323 100%);
  color: white;

  .header-cell {
    padding: 2rem;
    text-align: center;

    &.mufi {
      background: rgba(255,255,255,0.1);
      .logo {
        font-size: 1.5rem;
        font-weight: bold;
        margin-bottom: 0.5rem;
      }
      .tag {
        font-size: 0.9rem;
        opacity: 0.9;
      }
    }
  }
}

.table-row {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr;
  border-bottom: 1px solid rgba(0,0,0,0.1);
  transition: background-color 0.3s;

  &:hover {
    background-color: rgba(0,0,0,0.02);
  }

  > div {
    padding: 1.5rem;
    display: flex;
    align-items: center;
  }

  .feature-name {
    font-weight: 500;
    color: #1F1F1F;
  }

  .mufi-cell, .others-cell {
    display: flex;
    align-items: center;
    gap: 0.5rem;

    .icon {
      width: 20px;
      height: 20px;
      &.check {
        fill: #4CAF50;
      }
      &.cross {
        fill: #F44336;
      }
    }
  }

  .mufi-cell {
    background: rgba(76,175,80,0.1);
  }
}

.comparison-cta {
  text-align: center;
  margin-top: 3rem;

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

@include mobile {
  .comparison-table {
    margin: 0 1rem;
    font-size: 0.9rem;
  }

  .table-header, .table-row {
    grid-template-columns: 1fr;
  }

  .header-cell.empty {
    display: none;
  }

  .feature-name {
    background: rgba(0,0,0,0.05);
    font-weight: bold;
  }
}

.comparison-section {
  .highlight {
    color: #1F1F1F;
  }
  .comparison-item {
    &.active {
      background-color: #1F1F1F;
    }
  }
}
</style> 