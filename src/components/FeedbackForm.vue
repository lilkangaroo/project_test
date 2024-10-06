<template>
  <h2>Расскажите о вашем проекте:</h2>
  <form @submit.prevent="submitForm">
    <div>
      <label for="userName">Ваше имя*</label>
      <input
        id="userName"
        type="text"
        v-model="formData.userName"
        :class="{ invalid: errors.userName }"
      />
    </div>
    <div>
      <label for="userEmail">Email*</label>
      <input
        id="userEmail"
        type="email"
        v-model="formData.userEmail"
        :class="{ invalid: errors.userEmail }"
      />
    </div>
    <div>
      <label for="telNo">Телефон*</label>
      <input
        id="telNo"
        type="tel"
        v-model="formData.telNo"
        :class="{ invalid: errors.telNo }"
      />
    </div>
    <div>
      <label for="userMessage">Сообщение*</label>
      <input
        id="userMessage"
        type="text"
        v-model="formData.userMessage"
        :class="{ invalid: errors.userMessage }"
      />
    </div>
    <div>
      <label for="userApproval"
        >Согласие на обработку персональных данных</label
      >
      <input
        id="userApproval"
        type="checkbox"
        v-model="formData.userApproval"
      />
    </div>
    <div v-if="hasErrors" class="error-messages">
      <p>
        Поля обязательны для заполнения иначе мы не сможем с Вами связаться.
        Пожалуйста, заполните следующие поля:
      </p>
      <span v-if="errors.userName">{{ errors.userName }}</span>
      <span v-if="errors.userEmail">{{ errors.userEmail }}</span>
      <span v-if="errors.telNo">{{ errors.telNo }}</span>
      <span v-if="errors.userMessage">{{ errors.userMessage }}</span>
      <span v-if="errors.userApproval">{{ errors.userApproval }}</span>
    </div>

    <button type="submit">Обсудить проект</button>
  </form>
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

<style lang="scss"></style>
