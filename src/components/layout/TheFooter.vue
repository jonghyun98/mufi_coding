<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-grid">
        <div class="footer-info">
          <svg class="footer-logo" width="120" height="40" viewBox="0 0 120 40">
            <rect width="120" height="40" fill="#333"/>
            <text x="60" y="25" font-size="20" fill="white" text-anchor="middle">MUFI</text>
          </svg>
          <p>특별한 순간을 더욱 특별하게</p>
        </div>
        <div class="footer-links">
          <h4>바로가기</h4>
          <a href="#features">특징</a>
          <a href="#service">서비스</a>
          <a href="#cases">설치사례</a>
        </div>
        <div class="footer-social">
          <h4>SNS</h4>
          <div class="social-links">
            <a href="#" target="_blank" aria-label="Instagram">
              <svg viewBox="0 0 24 24" class="social-icon">
                <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
              </svg>
            </a>
            <a href="#" target="_blank" aria-label="Facebook">
              <svg viewBox="0 0 24 24" class="social-icon">
                <path d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z"/>
              </svg>
            </a>
            <a href="#" target="_blank" aria-label="YouTube">
              <svg viewBox="0 0 24 24" class="social-icon">
                <path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/>
              </svg>
            </a>
          </div>
        </div>
        <div class="footer-newsletter">
          <h4>뉴스레터 구독</h4>
          <form class="newsletter-form" @submit.prevent="handleSubscribe">
            <input type="email" placeholder="이메일 주소" v-model="email">
            <button type="submit">구독하기</button>
          </form>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2024 MUFI. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'TheFooter',
  data() {
    return {
      email: ''
    }
  },
  methods: {
    handleSubscribe() {
      // 뉴스레터 구독 로직 구현
      console.log('Newsletter subscription:', this.email)
    }
  }
}
</script>

<style lang="scss" scoped>
.footer {
  background: vars.$dark-color;
  color: white;
  padding: 4rem 0 2rem;
  word-break: keep-all;
  word-wrap: break-word;
}

.footer-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 3rem;
  margin-bottom: 3rem;
}

.footer-info {
  p {
    word-break: keep-all;
    word-wrap: break-word;
  }

  .footer-logo {
    height: 40px;
    margin-bottom: 1rem;
  }
}

.footer-links {
  h4 {
    margin-bottom: 1rem;
    word-break: keep-all;
  }

  a {
    display: block;
    color: white;
    text-decoration: none;
    margin: 0.5rem 0;
    opacity: 0.8;
    transition: opacity 0.3s;
    word-break: keep-all;
    word-wrap: break-word;

    &:hover {
      opacity: 1;
    }
  }
}

.social-links {
  display: flex;
  gap: 1rem;

  a {
    color: white;
    opacity: 0.8;
    transition: opacity 0.3s;

    &:hover {
      opacity: 1;
    }

    .social-icon {
      width: 24px;
      height: 24px;
      fill: currentColor;
    }
  }
}

.newsletter-form {
  display: flex;
  gap: 0.5rem;

  input {
    flex: 1;
    padding: 0.5rem;
    border: 1px solid rgba(255,255,255,0.2);
    border-radius: 4px;
    background: rgba(255,255,255,0.1);
    color: white;

    &::placeholder {
      color: rgba(255,255,255,0.6);
    }
  }

  button {
    padding: 0.5rem 1rem;
    background: vars.$primary-color;
    border: none;
    border-radius: 4px;
    color: white;
    cursor: pointer;
    transition: background 0.3s;

    &:hover {
      background: color.adjust(vars.$primary-color, $lightness: -10%);
    }
  }
}

.footer-bottom {
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid rgba(255,255,255,0.1);
  opacity: 0.8;
}

@include mixins.mobile {
  .footer-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .newsletter-form {
    flex-direction: column;
  }
}

.footer-newsletter {
  h4 {
    word-break: keep-all;
    margin-bottom: 1rem;
  }
}
</style>
