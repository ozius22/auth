<template>
  <div class="login-form">
    <div class="center">
      <h2 class="font-bold mb-10">Register</h2>
      <form @submit.prevent="handleRegister">
        <div class="form-group">
          <label for="name">Name</label>
          <input type="text" id="name" v-model="state.user.name" placeholder="Enter your name">
          <p>{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.name && state.errors._data.errors.name[0]}}</p>
        </div>
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
        <button type="submit">Register</button>
      </form>

      <p class="login"><nuxt-link href="/login">Already have an account?</nuxt-link></p>
    </div>
  </div>
</template>

<script setup>
  definePageMeta ({
    layout: 'form'
  })

import { reactive } from 'vue';

const state = reactive({
    errors: null,
    user:{
        name: null,
        email: null,
        password: null,
    }
})

async function handleRegister(){
    const params = {
        name: state.user.name,
        email: state.user.email,
        password: state.user.password,
    }

    try {
        const response = await $fetch(`http://127.0.0.1:8000/api/auth/register`, {
        method: 'POST',
        body: params
  })

  if (response.data){
    console.log('registered success!');
    console.log(response);
    localStorage.setItem('_token', response.data.token);
    navigateTo('/login');
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

  .login {
    margin-top: 80px;
  }

  .login {
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
  
  input[type="email"],
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
  