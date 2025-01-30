<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-grid">
        <div class="footer-info">
          <img :src="logoImage" alt="무피 로고" class="footer-logo"
            onerror="this.src='https://via.placeholder.com/120x40?text=MUFI'">
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
            <a href="#" target="_blank"><i class="icon-instagram"></i></a>
            <a href="#" target="_blank"><i class="icon-facebook"></i></a>
            <a href="#" target="_blank"><i class="icon-youtube"></i></a>
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
      email: '',
      logoImage: 'https://via.placeholder.com/120x40?text=MUFI'
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
}

.footer-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 3rem;
  margin-bottom: 3rem;
}

.footer-info {
  .footer-logo {
    height: 40px;
    margin-bottom: 1rem;
  }
}

.footer-links {
  h4 {
    margin-bottom: 1rem;
  }

  a {
    display: block;
    color: white;
    text-decoration: none;
    margin: 0.5rem 0;
    opacity: 0.8;
    transition: opacity 0.3s;

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
    font-size: 1.5rem;
    opacity: 0.8;
    transition: opacity 0.3s;

    &:hover {
      opacity: 1;
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
</style>
