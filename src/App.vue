<template>
  <main id="main">
    <h1>Password Checker!</h1>
    <form @submit.prevent="PasswordCheck" class="form">
      <label for="username">Username</label>
      <input type="text" name="username" id="username" v-model="username" />
      <label for="password">Password</label>
      <input type="password" name="password" id="password" v-model="password" />
      <button class="btn btn-primary">Login</button>
      <p v-if="badPassword" class="warning">{{ badMessage }}</p>
      <p v-if="goodPasssword" class="success">{{ goodMessage }}</p>
    </form>
  </main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      username: '',
      password: '',
      badPassword: false,
      goodPasssword: false,
      pattern: /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*()_+[\]{}|;:',.<>?/\\]).{8,}$/,
      badMessage: `The password must contain at least 8 characters.
The password must contain at least one uppercase letter (A-Z).
The password must contain at least one lowercase letter (a-z).
The password must contain at least one digit (0-9).
The password must contain at least one special character (e.g., !, @, #, $, %, ^, &, *).`,
      goodMessage: 'Password is good',
    }
  },
  methods: {
    PasswordCheck() {
      console.log('PasswordCheck called') // Debugging log to confirm method call
      if (!this.pattern.test(this.password) || this.password.length < 8) {
        console.log(this.password)
        this.badPassword = true
        this.goodPasssword = false
      } else {
        this.badPassword = false
        this.goodPasssword = true
      }
    },
  },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 300px;
  margin: 0 auto;
  gap: 0.5rem;
}

.btn {
  margin-top: 0.5rem;
  padding: 1rem;
  border-radius: 0.5rem;
  width: 10rem;
}
.warning {
  color: red;
}
.success {
  color: green;
}
h1 {
  text-align: center;
  margin-bottom: 3rem;
}
#main {
  display: grid;
  grid-template-columns: 1fr;
}
input {
  padding: 0.5rem;
  border-radius: 0.5rem;
  width: 100%;
}
</style>
