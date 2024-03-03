<template>
    <div class="login-form">
        <div class="center">
            <h2 class="font-bold mb-10">Login</h2>
  
            <form @submit.prevent="handleLogin">
                <div class="form-group">
                <label for="email">Email</label>
                <input type="text" id="email" v-model="state.user.email" placeholder="Enter your email">
                <p>{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.email && state.errors._data.errors.email[0]}}</p>
                </div>
                <div class="form-group">
                <label for="password">Password</label>
                <input type="password" id="password" v-model="state.user.password" placeholder="Enter your password">
                <p>{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.password && state.errors._data.errors.password[0]}}</p>
                </div>
                <button type="submit">Login</button>
            </form>
            
            <p class="register"><nuxt-link to="/register">Create an account</nuxt-link></p>
        </div>
    </div>
  </template>
  
  <script setup>
  definePageMeta ({
    layout: 'form'
  })
  
  const state = reactive({
      errors: null,
      user:{
          email: null,
          password: null,
      }
  })
  
  async function handleLogin(){
      const params = {
          email: state.user.email,
          password: state.user.password,
      }
  
      try {
          const response = await $fetch(`http://127.0.0.1:8000/api/auth/login`, {
          method: 'POST',
          body: params
    })
  
    if (response.data){
      localStorage.setItem('_token', response.data.token);
      navigateTo('/dashboard');
    }
      }
      catch (error){
          state.errors = error.response;
          console.log('error', error);
      }
  }
  </script>
  
  
  <style scoped>
    form div p {
        color: #FF7F7F;
    } 

    .register {
        margin-top: 80px;
    }

    .register a {
        color: blue;
    }
    
    .center {
        margin-top: 50px;
        display: flex;
        flex-direction: column; 
        align-items: center;
        justify-content: center;
    }

    .login-form {
        max-width: 600px;
        margin: 0 auto;
    }
    
    label {
        display: block;
        margin-bottom: 5px;
    }
    
    input[type="text"],
    input[type="password"] {
        width: 100%;
        padding: 10px;
        font-size: 16px;
        border-radius: 5px;
        border: 1px solid #ccc;
    }
    
    button {
        display: block;
        margin: 30px auto;
        padding: 8px 30px;
        font-size: 16px;
        border-radius: 5px;
        border: 1px solid #ccc;
        background-color: white;
        color: gray;
        cursor: pointer;
    }
    
    button:hover {
        background-color: lightgray;
        color: white;
    }
  </style>
  