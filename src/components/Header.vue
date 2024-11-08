<template>
    <nav class="navbar">
        <a href="/" class="nav-link">Home</a>
        <a href="/add-restaurant" class="nav-link">Add Restaurant</a>
        <a href="/update-restaurant" class="nav-link">Update Restaurant</a>
        <button @click="logout" class="nav-link">Logout</button>
    </nav>
  </template>
  
  <script>
  export default {
    name: "Header",
    methods:  {
        logout () {
            localStorage.clear();
            this.$router.push({name:'login'});
        }
    }
  };
  </script>
  
  <style scoped>
  .navbar {
    background-color: #333;
    overflow: hidden;
  }
  
  .navbar a {
    float: left;
    color: #f1f2f0;
    padding: 14px 16px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
  }
  
  button {
    text-decoration: none;
    float: right;
    width: 150px;
  }
  </style>
  