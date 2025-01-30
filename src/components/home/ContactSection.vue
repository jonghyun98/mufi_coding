<template>
  <section id="contact" class="contact">
    <div class="container">
      <div class="contact-grid">
        <div class="contact-info">
          <h2>문의하기</h2>
          <p>무피와 함께 특별한 순간을 만들어보세요</p>
          <div class="contact-details">
            <div class="contact-item">
              <i class="icon-phone"></i>
              <p>1544-0000</p>
            </div>
            <div class="contact-item">
              <i class="icon-email"></i>
              <p>contact@mufi.co.kr</p>
            </div>
          </div>
        </div>
        <form class="contact-form" @submit.prevent="handleSubmit">
          <div class="form-group">
            <input type="text" placeholder="이름" required v-model="form.name">
          </div>
          <div class="form-group">
            <input type="email" placeholder="이메일" required v-model="form.email">
          </div>
          <div class="form-group">
            <select required v-model="form.type">
              <option value="">문의 유형 선택</option>
              <option value="purchase">구매 문의</option>
              <option value="rental">렌탈 문의</option>
              <option value="partnership">제휴 문의</option>
            </select>
          </div>
          <div class="form-group">
            <textarea placeholder="문의내용" required v-model="form.message"></textarea>
          </div>
          <button type="submit" class="submit-btn">문의하기</button>
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
        type: '',
        message: ''
      }
    }
  },
  methods: {
    handleSubmit() {
      // 폼 제출 로직 구현
      console.log('Form submitted:', this.form)
    }
  }
}
</script>

<style lang="scss" scoped>
.contact {
  background: vars.$light-color;
  padding: 5rem 0;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
}

.contact-info {
  h2 {
    text-align: left;
    color: vars.$dark-color;
  }

  p {
    color: vars.$dark-color;
    margin-bottom: 2rem;
  }
}

.contact-details {
  .contact-item {
    display: flex;
    align-items: center;
    margin: 1rem 0;
    
    i {
      margin-right: 1rem;
      color: vars.$primary-color;
    }
  }
}

.contact-form {
  .form-group {
    margin-bottom: 1.5rem;

    input,
    select,
    textarea {
      width: 100%;
      padding: 1rem;
      border: 1px solid #ddd;
      border-radius: 5px;
      font-family: inherit;
      
      &:focus {
        outline: none;
        border-color: vars.$primary-color;
      }
    }

    textarea {
      height: 150px;
      resize: vertical;
    }
  }

  .submit-btn {
    background: vars.$primary-color;
    color: white;
    padding: 1rem 2rem;
    border: none;
    border-radius: 25px;
    cursor: pointer;
    transition: background 0.3s;

    &:hover {
      background: color.adjust(vars.$primary-color, $lightness: -10%);
    }
  }
}

@include mixins.mobile {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
}
</style> 