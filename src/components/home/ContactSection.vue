<template>
  <section id="contact" class="contact">
    <div class="container">
      <h2>문의하기</h2>
      <p class="section-desc">무피와 함께 특별한 순간을 만들어보세요</p>

      <div class="contact-grid">
        <div class="contact-info">
          <div class="info-item">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
            </svg>
            <div class="info-content">
              <h3>이메일</h3>
              <p><a href="mailto:ghtnakdmf123@gmail.com">ghtnakdmf123@gmail.com</a></p>
            </div>
          </div>
          <div class="info-item">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M20 10.999h2C22 5.869 18.127 2 12.99 2v2C17.052 4 20 6.943 20 10.999z"/>
              <path d="M13 8c2.103 0 3 .897 3 3h2c0-3.225-1.775-5-5-5v2zm3.422 5.443c-.354-.424-.427-.935-.422-1.443.002-.361.054-.719.161-1.061.164-.519.407-.973.72-1.377.369-.477.455-1.127.229-1.707-.226-.579-.737-.975-1.353-1.047-.247-.029-.497-.042-.747-.042-2.012 0-4.179.969-4.179 3.234 0 3.403 4.065 6.801 5.627 7.965.124.093.343.146.6.146.268 0 .488-.054.612-.147 1.342-.996 4.819-3.889 5.33-6.414.174-.858-.226-1.804-.945-2.184l-2.435 2.434-3.198.643z"/>
            </svg>
            <div class="info-content">
              <h3>전화</h3>
              <p><a href="tel:010-5547-0355">010-5547-0355</a></p>
            </div>
          </div>
          <div class="info-item">
            <svg viewBox="0 0 24 24" class="icon">
              <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/>
            </svg>
            <div class="info-content">
              <h3>주소</h3>
              <p>서울특별시 강남구 테헤란로</p>
            </div>
          </div>
        </div>

        <form class="contact-form" @submit.prevent="handleSubmit">
          <div class="form-group">
            <label for="name">이름</label>
            <input type="text" id="name" v-model="form.name" required>
          </div>
          <div class="form-group">
            <label for="email">이메일</label>
            <input type="email" id="email" v-model="form.email" required>
          </div>
          <div class="form-group">
            <label for="phone">연락처</label>
            <input type="tel" id="phone" v-model="form.phone" required>
          </div>
          <div class="form-group">
            <label for="type">문의 유형</label>
            <select id="type" v-model="form.type" required>
              <option value="">선택해주세요</option>
              <option value="purchase">구매 문의</option>
              <option value="rental">렌탈 문의</option>
              <option value="partnership">제휴 문의</option>
              <option value="other">기타 문의</option>
            </select>
          </div>
          <div class="form-group">
            <label for="message">문의 내용</label>
            <textarea id="message" v-model="form.message" rows="5" required></textarea>
          </div>
          <button type="submit" class="btn primary">문의하기</button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ContactSection',
  data() {
    return {
      form: {
        name: '',
        email: '',
        phone: '',
        type: '',
        message: ''
      }
    }
  },
  methods: {
    handleSubmit() {
      // mailto 링크 생성
      const subject = `[무피 문의] ${this.form.type} - ${this.form.name}님`;
      const body = `
이름: ${this.form.name}
이메일: ${this.form.email}
연락처: ${this.form.phone}
문의 유형: ${this.form.type}

문의 내용:
${this.form.message}
      `.trim();

      // mailto 링크 열기
      window.location.href = `mailto:ghtnakdmf123@gmail.com?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
      
      // 폼 초기화
      this.form = {
        name: '',
        email: '',
        phone: '',
        type: '',
        message: ''
      };
    }
  }
}
</script>

<style lang="scss" scoped>
.contact {
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

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 4rem;
  max-width: 1200px;
  margin: 0 auto;
}

.contact-info {
  .info-item {
    display: flex;
    align-items: center;
    margin-bottom: 2rem;
    padding: 1.5rem;
    background: rgba(31, 31, 31, 0.05);
    border-radius: 10px;
    transition: transform 0.3s;

    &:hover {
      transform: translateX(10px);
    }

    .icon {
      width: 32px;
      height: 32px;
      margin-right: 1rem;
      fill: #1F1F1F;
    }

    .info-content {
      h3 {
        font-size: 1.1rem;
        margin-bottom: 0.5rem;
        color: #1F1F1F;
      }

      p {
        color: #1F1F1F;
        opacity: 0.8;
        a {
          color: #1F1F1F;
          text-decoration: none;
          transition: color 0.3s;

          &:hover {
            color: #1F1F1F;
          }
        }
      }
    }
  }
}

.contact-form {
  background: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);

  .form-group {
    margin-bottom: 1.5rem;

    label {
      display: block;
      margin-bottom: 0.5rem;
      color: #1F1F1F;
      font-weight: 500;
    }

    input, select, textarea {
      width: 100%;
      padding: 0.75rem;
      border: 1px solid rgba(0,0,0,0.1);
      border-radius: 5px;
      font-size: 1rem;
      transition: border-color 0.3s;

      &:focus {
        outline: none;
        border-color: #1F1F1F;
      }
    }

    textarea {
      resize: vertical;
    }
  }

  .btn.primary {
    width: 100%;
    padding: 1rem;
    font-size: 1.1rem;
    background: #1F1F1F;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: transform 0.3s;

    &:hover {
      transform: translateY(-2px);
    }
  }
}

@include mixins.mobile {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
    padding: 0 1rem;
  }

  .contact-info .info-item {
    margin: 0 1rem 1rem;
  }
}
</style> 