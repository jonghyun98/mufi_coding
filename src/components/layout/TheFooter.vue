<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <h3>MUFI</h3>
          <p class="company-desc">특별한 순간을 더욱 특별하게</p>
          <div class="social-links">
            <a href="#" target="_blank" rel="noopener" aria-label="Instagram">
              <svg viewBox="0 0 24 24">
                <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
              </svg>
            </a>
            <a href="#" target="_blank" rel="noopener" aria-label="Facebook">
              <svg viewBox="0 0 24 24">
                <path d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z"/>
              </svg>
            </a>
          </div>
        </div>
        <div class="footer-section">
          <h4>Contact</h4>
          <ul>
            <li>
              <svg viewBox="0 0 24 24">
                <path d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
              </svg>
              <a href="mailto:ghtnakdmf123@gmail.com">ghtnakdmf123@gmail.com</a>
            </li>
            <li>
              <svg viewBox="0 0 24 24">
                <path d="M6.62 10.79c1.44 2.83 3.76 5.14 6.59 6.59l2.2-2.2c.27-.27.67-.36 1.02-.24 1.12.37 2.33.57 3.57.57.55 0 1 .45 1 1V20c0 .55-.45 1-1 1-9.39 0-17-7.61-17-17 0-.55.45-1 1-1h3.5c.55 0 1 .45 1 1 0 1.25.2 2.45.57 3.57.11.35.03.74-.25 1.02l-2.2 2.2z"/>
              </svg>
              <a href="tel:010-5547-0355">010-5547-0355</a>
            </li>
          </ul>
        </div>
        <div class="footer-section">
          <h4>Quick Links</h4>
          <ul>
            <li><a href="#features">서비스 소개</a></li>
            <li><a href="#kiosk">키오스크</a></li>
            <li><a href="#cases">설치 사례</a></li>
            <li><a href="#contact">문의하기</a></li>
          </ul>
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
  background: #1F1F1F;
  color: white;
  padding: 4rem 0 2rem;

  .footer-content {
    display: grid;
    grid-template-columns: 2fr 1.5fr 1fr;
    gap: 4rem;
    margin-bottom: 3rem;
  }

  .footer-section {
    h3 {
      font-size: 1.8rem;
      margin-bottom: 1rem;
    }

    h4 {
      font-size: 1.2rem;
      margin-bottom: 1.5rem;
    }

    .company-desc {
      opacity: 0.8;
      margin-bottom: 2rem;
    }

    ul {
      list-style: none;
      padding: 0;

      li {
        margin-bottom: 1rem;
        display: flex;
        align-items: center;

        svg {
          width: 20px;
          height: 20px;
          fill: white;
          margin-right: 0.8rem;
          opacity: 0.8;
        }

        a {
          color: white;
          text-decoration: none;
          opacity: 0.8;
          transition: opacity 0.3s;

          &:hover {
            opacity: 1;
          }
        }
      }
    }
  }

  .social-links {
    display: flex;
    gap: 1rem;

    a {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 40px;
      height: 40px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 50%;
      transition: all 0.3s;

      svg {
        width: 20px;
        height: 20px;
        fill: white;
      }

      &:hover {
        background: white;
        
        svg {
          fill: #1F1F1F;
        }
      }
    }
  }

  .footer-bottom {
    text-align: center;
    padding-top: 2rem;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    
    p {
      opacity: 0.6;
      font-size: 0.9rem;
    }
  }
}

@include mixins.mobile {
  .footer {
    padding: 3rem 1rem 1.5rem;

    .footer-content {
      grid-template-columns: 1fr;
      gap: 2rem;
      text-align: center;
    }

    .social-links {
      justify-content: center;
    }

    .footer-section ul li {
      justify-content: center;
    }
  }
}
</style>
