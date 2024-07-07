<template>
  <div class="register-form">
    <h1>Register</h1>
    <form @submit.prevent="submitForm">
      <div>
        <input v-model="username" placeholder="Username" />
        <p v-if="errors.username">{{ errors.username }}</p>
      </div>
      <div>
        <input v-model="email" placeholder="Email" />
        <p v-if="errors.email">{{ errors.email }}</p>
      </div>
      <div>
        <input type="password" v-model="password" placeholder="Password" />
        <p v-if="errors.password">{{ errors.password }}</p>
      </div>
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script>
export default {
    name:"Register",
    data() {
        return {
        username: '',
        email: '',
        password: '',
        errors: {}
        };
    },
    methods: {
        submitForm() {
        this.errors = {};

        if (!this.username) {
            this.errors.username = 'Username is required.';
        }

        if (!this.email) {
            this.errors.email = 'Email is required.';
        } else if (!this.validEmail(this.email)) {
            this.errors.email = 'Email is invalid.';
        }

        if (!this.password) {
            this.errors.password = 'Password is required.';
        }

        if (Object.keys(this.errors).length === 0) {
            alert('Form submitted successfully!');
        }
        },
        validEmail(email) {
        const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@(([^<>()[\]\.,;:\s@"]+\.[^<>()[\]\.,;:\s@"]{2,})*)$/i;
        return re.test(email.toLowerCase());
        }
    }
    };
</script>

<style scoped>
    .register-form {
    text-align: center;
    }

    input {
    display: block;
    margin: 10px auto;
    padding: 10px;
    width: 80%;
    max-width: 300px;
    }

    button {
    padding: 10px 20px;
    margin-top: 10px;
    }

    p {
    color: red;
    font-size: 12px;
    }
</style>
