<template>
  <div class="container">
    <img width="50px" src="../assets/logo.svg" alt="LOGO">
    <h1>Register</h1>
    <form @submit.prevent="register">
      <label for="name">Name:</label>
      <input type="text" name="name" v-model="name" id="name" placeholder="John DOE" required>

      <label for="email">Email:</label>
      <input type="email" name="email" v-model="email" id="email" placeholder="example@gmail.com" required>

      <label for="password">Password:</label>
      <input type="password" name="password" v-model="password" id="password" placeholder="password" required>

      <button type="submit">Register</button>
    </form>
      <router-link to="/login" class="link-button">Login</router-link>
    </div> 
</template>

<script>
import axios from 'axios';

export default {
  name: 'Register',
  data() {
    return {
      name: '',
      email: '',
      password: ''
    };
  },
  methods: {
    async register() {
      if (this.name && this.email && this.password) {

        let result = await axios.post("http://localhost:3000/user", {
          name:this.name,
          email:this.email,
          password:this.password,
        });
        console.warn(result);

        if(result.status == 201) {
          console.log("Registration successfully");
          localStorage.setItem("user-info",JSON.stringify(result.data));
          this.$router.push({name:'home'});
        }
        else {

        }
      } else {
        console.warn("All fields are required");
      }
    }
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
</style>
