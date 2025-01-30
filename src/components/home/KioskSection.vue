<template>
  <section id="kiosk" class="kiosk">
    <div class="container">
      <h2>무피 키오스크</h2>
      <div class="kiosk-content">
        <div class="kiosk-info">
          <h3>스마트한 네컷사진관의 시작</h3>
          <ul class="kiosk-features">
            <li>
              <svg viewBox="0 0 24 24" class="icon">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
              </svg>
              직관적인 UI/UX로 누구나 쉽게 사용
            </li>
            <li>
              <svg viewBox="0 0 24 24" class="icon">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
              </svg>
              빠른 결제 시스템 탑재
            </li>
            <li>
              <svg viewBox="0 0 24 24" class="icon">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
              </svg>
              실시간 데이터 분석 및 관리
            </li>
            <li>
              <svg viewBox="0 0 24 24" class="icon">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
              </svg>
              다양한 프레임과 필터 옵션
            </li>
          </ul>
          <div class="kiosk-specs">
            <h4>주요 스펙</h4>
            <div class="specs-grid">
              <div class="spec-item">
                <span class="label">디스플레이</span>
                <span class="value">32인치 터치스크린</span>
              </div>
              <div class="spec-item">
                <span class="label">카메라</span>
                <span class="value">4K 고화질</span>
              </div>
              <div class="spec-item">
                <span class="label">프린터</span>
                <span class="value">고속 열전사 방식</span>
              </div>
              <div class="spec-item">
                <span class="label">결제</span>
                <span class="value">카드/간편결제</span>
              </div>
            </div>
          </div>
          <div class="kiosk-buttons">
            <button class="btn primary">구매 문의</button>
            <button class="btn secondary">렌탈 문의</button>
          </div>
        </div>
        <div class="kiosk-image">
          <div class="placeholder-image">
            <span>MUFI Kiosk</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.kiosk {
  background: linear-gradient(135deg, #1a237e 0%, #283593 100%);
  color: white;
  padding: 5rem 0;

  h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 3rem;
    color: white;
  }
}

.kiosk-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.kiosk-info {
  h3 {
    font-size: 2rem;
    margin-bottom: 2rem;
  }

  .kiosk-features {
    list-style: none;
    margin: 2rem 0;
    padding: 0;

    li {
      display: flex;
      align-items: center;
      margin: 1rem 0;
      font-size: 1.1rem;

      .icon {
        width: 24px;
        height: 24px;
        margin-right: 1rem;
        fill: vars.$primary-color;
      }
    }
  }
}

.kiosk-specs {
  background: rgba(255, 255, 255, 0.1);
  padding: 2rem;
  border-radius: 10px;
  margin: 2rem 0;

  h4 {
    margin-bottom: 1.5rem;
    font-size: 1.2rem;
  }

  .specs-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
  }

  .spec-item {
    .label {
      display: block;
      font-size: 0.9rem;
      opacity: 0.8;
      margin-bottom: 0.5rem;
    }

    .value {
      font-size: 1.1rem;
      font-weight: 500;
    }
  }
}

.kiosk-buttons {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;

  .btn {
    padding: 1rem 2rem;
    border: none;
    border-radius: 25px;
    font-size: 1rem;
    cursor: pointer;
    transition: transform 0.3s;

    &:hover {
      transform: translateY(-2px);
    }

    &.primary {
      background: vars.$primary-color;
      color: white;
    }

    &.secondary {
      background: transparent;
      border: 2px solid white;
      color: white;
    }
  }
}

.kiosk-image {
  .placeholder-image {
    width: 100%;
    height: 500px;
    background: rgba(255, 255, 255, 0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    font-size: 1.5rem;
    color: white;
  }
}

@include mixins.mobile {
  .kiosk-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .kiosk-specs .specs-grid {
    grid-template-columns: 1fr;
  }

  .kiosk-buttons {
    flex-direction: column;
  }
}
</style> 