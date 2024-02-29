<template>
    <div class="login-form">
        <div class="center">
            <h2>Login</h2>
            <form @submit.prevent="handleLogin">
                <div class="form-group">
                <label for="email">Email</label>
                <input type="email" id="email" v-model="state.user.email" placeholder="Enter your email">
                <p>{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.email && state.errors._data.errors.email[0]}}</p>
                </div>
                <div class="form-group">
                <label for="password">Password</label>
                <input type="password" id="password" v-model="state.user.password" placeholder="Enter your password">
                <p>{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.password && state.errors._data.errors.password[0]}}</p>
                </div>
                <button type="submit">Login</button>
            </form>
        </div>
    </div>
  </template>
  
  <script setup>
  
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
    .center {
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
  input[type="password"] {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  
  button {
    display: block;
    margin: 0 auto;
    padding: 10px 15px;
    font-size: 16px;
    border-radius: 5px;
    border: none;
    color: gray;
    cursor: pointer;
  }
  
  button:hover {
    background-color: white;
  }
  
  @media (max-width: 768px) {
    .login-form {
      max-width: 300px;
    }
  }
  </style>
  