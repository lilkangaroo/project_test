<template>
  <section class="form">
    <h1>
      Расскажите <br />
      о вашем проекте:
    </h1>
    <form @submit.prevent="submitForm" class="form__container">
      <div class="form__input-group">
        <div class="form__group">
          <label for="userName" class="form__label">Ваше имя*</label>
          <input
            id="userName"
            type="text"
            v-model="formData.userName"
            :class="{ 'form__input--invalid': errors.userName }"
            class="form__input"
          />
        </div>
        <div class="form__group">
          <label for="userEmail" class="form__label">Email*</label>
          <input
            id="userEmail"
            type="email"
            v-model="formData.userEmail"
            :class="{ 'form__input--invalid': errors.userEmail }"
            class="form__input"
          />
        </div>
        <div class="form__group">
          <label for="telNo" class="form__label">Телефон*</label>
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
        <label for="userMessage" class="form__label">Сообщение*</label>
        <textarea
          id="userMessage"
          v-model="formData.userMessage"
          :class="{ 'form__input--invalid': errors.userMessage }"
          class="form__input form__input--message"
        ></textarea>
      </div>
      <div class="form__checkbox">
        <input
          id="userApproval"
          type="checkbox"
          v-model="formData.userApproval"
          class="form__input-checkbox"
        />
        <label for="userApproval" class="form__label">
          Согласие на обработку персональных данных
        </label>
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

      <button type="submit" class="form__button">Обсудить проект</button>
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
    };
  },
  methods: {
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
        this.errors.userName = 'Имя';
        valid = false;
      }
      if (!this.formData.userEmail) {
        this.errors.userEmail = 'Email';
        valid = false;
      }
      if (!this.formData.telNo) {
        this.errors.telNo = 'Телефон';
        valid = false;
      }
      if (!this.formData.userMessage) {
        this.errors.userMessage = 'Сообщение';
        valid = false;
      }
      if (!this.formData.userApproval) {
        this.errors.userApproval = 'Согласие на обработку персональных данных.';
        valid = false;
      }

      return valid;
    },
    async submitForm() {
      if (!this.validate()) return;

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
    top: -10px;
    left: 10px;
    background-color: $background-color;
    padding: 0 5px;
    font-size: 14px;
    color: $color-text;

    @media (max-width: 480px) {
      font-size: 12px;
      top: -8px;
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

    &--invalid {
      border-color: $color-error;
    }

    &--message {
      width: 100%;
      height: 150px;
    }
  }

  @media (max-width: 480px) {
    padding: 10px; /* Уменьшаем внутренние отступы */

    &--message {
      height: 100px; /* Уменьшаем высоту для мобильных */
    }
  }

  &__checkbox {
    display: flex;
    align-items: center;
    gap: 10px;

    .form__label {
      position: static;
      background-color: transparent;
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

  @media (max-width: 480px) {
    width: 150px;
    height: 40px;
    font-size: 14px;
  }

  &__error-messages {
    color: $color-error;
  }

  &__error-text {
    margin-bottom: 10px;
  }
  @media (max-width: 480px) {
    &__container {
      margin-bottom: 40px;
      gap: 15px;
    }

    &__group {
      margin-bottom: 15px;
    }
  }
}
</style>
