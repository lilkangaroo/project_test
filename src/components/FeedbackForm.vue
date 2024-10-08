<template>
  <section class="form">
    <div class="form__header">
      <img
        v-if="isMobile"
        src="../img/form_img.png"
        alt="Описание картинки"
        class="form__image"
      />
      <h1>
        Расскажите <br />
        о вашем проекте:
      </h1>
    </div>
    <form @submit.prevent="submitForm" class="form__container">
      <div class="form__input-group">
        <div class="form__group">
          <label
            for="userName"
            class="form__label"
            :class="{ 'form__label--hidden': isMobile && formData.userName }"
          >
            Ваше имя*
          </label>
          <input
            id="userName"
            type="text"
            v-model="formData.userName"
            :class="{ 'form__input--invalid': errors.userName }"
            class="form__input"
          />
        </div>
        <div class="form__group">
          <label
            for="userEmail"
            class="form__label"
            :class="{ 'form__label--hidden': isMobile && formData.userEmail }"
          >
            Email*
          </label>
          <input
            id="userEmail"
            type="email"
            v-model="formData.userEmail"
            :class="{ 'form__input--invalid': errors.userEmail }"
            class="form__input"
          />
        </div>
        <div class="form__group">
          <label
            for="telNo"
            class="form__label"
            :class="{ 'form__label--hidden': isMobile && formData.telNo }"
          >
            Телефон*
          </label>
          <input
            id="telNo"
            type="tel"
            v-model="formData.telNo"
            :class="{ 'form__input--invalid': errors.telNo }"
            class="form__input"
          />
        </div>
      </div>
      <div class="form__group form__message">
        <label
          for="userMessage"
          class="form__label"
          :class="{ 'form__label--hidden': isMobile && formData.userMessage }"
        >
          Сообщение*
        </label>
        <textarea
          id="userMessage"
          v-model="formData.userMessage"
          :class="{ 'form__input--invalid': errors.userMessage }"
          class="form__input form__input--message"
        ></textarea>
      </div>

      <div v-if="!isMobile">
        <div class="form__checkbox">
          <input
            id="userApproval"
            type="checkbox"
            v-model="formData.userApproval"
            class="form__input-checkbox"
          />
          <label for="userApproval" class="form__label form__label--checkbox">
            Согласие на обработку персональных данных
          </label>
        </div>
      </div>

      <div v-if="hasErrors" class="form__error-messages">
        <p class="form__error-text">
          Поля обязательны для заполнения, иначе мы не сможем с Вами связаться.
          Пожалуйста, заполните следующие поля:
        </p>
        <ul>
          <li v-if="errors.userName">{{ errors.userName }}</li>
          <li v-if="errors.userEmail">{{ errors.userEmail }}</li>
          <li v-if="errors.telNo">{{ errors.telNo }}</li>
          <li v-if="errors.userMessage">{{ errors.userMessage }}</li>
          <li v-if="errors.userApproval">{{ errors.userApproval }}</li>
        </ul>
      </div>

      <button type="submit" class="form__button">
        {{ isMobile ? 'ОТПРАВИТЬ' : 'Обсудить проект' }}
      </button>

      <p v-if="isMobile" class="form__consent-text">
        Нажимая “Отправить”, Вы даете согласие на обработку персональных данных.
      </p>
    </form>
  </section>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      formData: {
        userName: '',
        userEmail: '',
        telNo: '',
        userMessage: '',
        userApproval: false,
      },
      errors: {
        userName: null,
        userEmail: null,
        telNo: null,
        userMessage: null,
        userApproval: null,
      },
      isMobile: false,
    };
  },
  created() {
    this.checkIfMobile();
  },
  methods: {
    checkIfMobile() {
      this.isMobile = window.innerWidth <= 480;
    },
    clearForm() {
      this.formData = {
        userName: '',
        userEmail: '',
        telNo: '',
        userMessage: '',
        userApproval: false,
      };
      this.errors = {
        userName: null,
        userEmail: null,
        telNo: null,
        userMessage: null,
        userApproval: null,
      };
    },
    validate() {
      this.errors = {};
      let valid = true;

      if (!this.formData.userName) {
        this.errors.userName = 'Имя обязательно для заполнения.';
        valid = false;
      }
      if (!this.formData.userEmail) {
        this.errors.userEmail = 'Email обязателен для заполнения.';
        valid = false;
      }
      if (!this.formData.telNo) {
        this.errors.telNo = 'Телефон обязателен для заполнения.';
        valid = false;
      }
      if (!this.formData.userMessage) {
        this.errors.userMessage = 'Сообщение обязательно для заполнения.';
        valid = false;
      }

      if (!this.isMobile && !this.formData.userApproval) {
        this.errors.userApproval =
          'Необходимо согласие на обработку персональных данных.';
        valid = false;
      }

      return valid;
    },
    async submitForm() {
      if (!this.validate()) return;

      if (this.isMobile) {
        this.formData.userApproval = true;
      }

      try {
        await axios.post('https://api.test.cyberia.studio/api/v1/feedbacks', {
          name: this.formData.userName,
          email: this.formData.userEmail,
          phone: this.formData.telNo,
          message: this.formData.userMessage,
        });
        alert('Обращение принято!');
        this.clearForm();
      } catch (error) {
        if (error.response && error.response.status === 422) {
          this.handleServerValidationErrors(error.response.data.errors);
        } else {
          alert('Произошла ошибка при отправке формы.');
        }
      }
    },
    handleServerValidationErrors(errors) {
      if (errors.name) {
        this.errors.userName = errors.name[0];
      }
      if (errors.email) {
        this.errors.userEmail = errors.email[0];
      }
      if (errors.phone) {
        this.errors.telNo = errors.phone[0];
      }
      if (errors.message) {
        this.errors.userMessage = errors.message[0];
      }
    },
  },
  computed: {
    hasErrors() {
      return Object.values(this.errors).some((error) => error !== null);
    },
  },
};
</script>

<style lang="scss">
.form {
  &__header {
    display: flex;
    align-items: center;
    gap: 10px;

    @media (max-width: 480px) {
      flex-direction: row;
    }
  }

  &__image {
    display: none;

    @media (max-width: 480px) {
      display: block;
      width: 50px;
      height: auto;
    }
  }

  &__container {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-bottom: 70px;
  }

  &__input-group {
    display: flex;
    gap: 20px;
    justify-content: space-between;

    @media (max-width: 480px) {
      flex-direction: column;
      gap: 10px;
    }
  }

  &__group {
    position: relative;
    flex: 1;
    margin-bottom: 20px;
  }

  &__label {
    position: absolute;
    top: 50%;
    left: 15px;
    transform: translateY(-50%);
    font-size: 14px;
    color: $color-text;
    pointer-events: none;
    transition: 0.2s;
    background-color: $background-color;

    @media (max-width: 480px) {
      top: 50%;
      left: 15px;
    }
  }

  &__input {
    padding: 15px;
    border: 1px solid $color-text;
    background-color: $background-color;
    color: $color-text-white;
    border-radius: 5px;
    width: 100%;
    box-sizing: border-box;
    font-size: $text-size-mob;

    &:focus + .form__label,
    &:not(:placeholder-shown) + .form__label {
      top: -10px;
      font-size: $text-size-mob;
      color: $color-text;
    }
  }

  &__checkbox {
    display: flex;
    align-items: center;
    gap: 10px;

    .form__label--checkbox {
      position: static;
      background-color: transparent;
      margin: 0;
      color: $color-text;
      font-size: $text-size-mob;
    }
  }

  &__button {
    display: block;
    padding: 10px 20px;
    border: none;
    background-color: $color-button-form;
    color: $color-text-white;
    cursor: pointer;
    border-radius: 50px;
    margin: 0 auto;
    font-size: $text-size;
    width: 200px;
    height: 50px;
  }

  &__consent-text {
    margin-top: 10px;
    font-size: $text-size;
    color: $color-text;
    text-align: center;
  }

  @media (max-width: 480px) {
    padding: 20px;
  }
}
</style>
