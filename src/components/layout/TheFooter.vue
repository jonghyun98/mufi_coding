<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <h3>MUFI</h3>
          <p>특별한 순간을 더욱 특별하게</p>
        </div>
        <div class="footer-section">
          <h4>Contact</h4>
          <p>Email: ghtnakdmf123@gmail.com</p>
          <p>Tel: 010-5547-0355</p>
        </div>
        <div class="footer-section">
          <h4>Follow Us</h4>
          <div class="social-links">
            <a href="#" target="_blank" rel="noopener">Instagram</a>
            <a href="#" target="_blank" rel="noopener">Facebook</a>
          </div>
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
  background: #1a237e;
  color: white;
  padding: 4rem 0 2rem;
  margin-top: 4rem;

  .footer-content {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
    margin-bottom: 3rem;
  }

  .footer-section {
    h3, h4 {
      font-size: 1.2rem;
      margin-bottom: 1rem;
    }

    p {
      opacity: 0.8;
      margin-bottom: 0.5rem;
    }
  }

  .social-links {
    display: flex;
    gap: 1rem;

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

  .footer-bottom {
    text-align: center;
    padding-top: 2rem;
    border-top: 1px solid rgba(255,255,255,0.1);
    
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
      text-align: center;
    }

    .social-links {
      justify-content: center;
    }
  }
}
</style>
