<template>
  <div class="login-form">
    <h2>Login</h2>
    <form @submit.prevent="handleRegister">
      <div class="form-group">
        <label for="name">Name</label>
        <input type="name" id="name" v-model="state.user.name" placeholder="Enter your name">
        <p>{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.name && state.errors._data.errors.name[0]}}</p>
      </div>
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
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script setup>

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
    navigateTo('/');
  }
    }
    catch (error){
        state.errors = error.response;
        console.log('error', error);
    }
}
</script>


<style scoped>
.login-form {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.form-group {
  margin-bottom: 15px;
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
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: none;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

@media (max-width: 768px) {
  .login-form {
    max-width: 300px;
  }
}
</style>
