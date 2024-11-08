<template>
  <div class="container">
    <img width="50px" src="../assets/logo.svg" alt="LOGO">
    <h1>Login</h1>
    <form @submit.prevent="login">
      <label for="email">Email:</label>
      <input
        type="email"
        name="email"
        v-model="email"
        id="email"
        placeholder="example@gmail.com"
        required
      />

      <label for="password">Password:</label>
      <input
        type="password"
        name="password"
        v-model="password"
        id="password"
        placeholder="password"
        required
      />

      <button type="submit">Login</button>
    </form>
    <router-link to="/register" class="link-button">Register</router-link>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    async login() {
      if (this.email && this.password) {
        try {
          let result = await axios.get(`http://localhost:3000/user?email=${this.email}&password=${this.password}`);
          console.warn(result);

          if (result.status === 200 && result.data.length > 0) {
            console.log("Login successful");
            localStorage.setItem("user-info", JSON.stringify(result.data));
            this.$router.push({ name: 'home' });
          } else {
            console.error("Login failed. Please check your credentials.");
          }
        } catch (error) {
          console.error("An error occurred:", error.message);
        }
      } else {
        console.warn("All fields are required");
      }
    },
  },
  mounted() {
    let user=localStorage.getItem("user-info");
    if(user) {
      this.$router.push({name:'home'});
    }
  }
};
</script>

<style scoped>
.container {
  margin: auto;
  justify-content: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.container img,
.container h1 {
  text-align: center;
}

form {
  width: 100%;
}

form label {
  display: block;
  margin: 0.5rem 0 0.2rem;
}

form input {
  width: 100%;
  padding: 0.5rem;
  margin-bottom: 1rem;
  border: 1px solid #ccc;
  border-radius: 3px;
}

button {
  padding: 0.5rem 1rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  width: 100%;
}

button:hover {
  opacity: 0.8;
}

.link-button {
  display: block;
  text-align: center;
  margin-top: 1rem;
  color: #007bff;
  text-decoration: none;
  cursor: pointer;
}

.link-button:hover {
  text-decoration: underline;
}
</style>
