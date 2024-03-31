<template>
    <div class="flex justify-center items-center h-screen">
        <div class="w-full max-w-md -mt-28">
            <h1 class="text-center block text-gray-700 text-lg font-bold mb-2">Log In</h1>
            <Form @submit="handleLogin()" class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="email">Email</label>
                    <Field type="text"
                        name="email"
                        placeholder="Enter your email"
                        class="w-full px-3 py-2 border rounded-md shadow-sm focus:outline-none focus:border-blue-500 focus:ring focus:ring-blue-500"
                        :rules="validateEmail"
                        v-model="state.user.email"
                    />
                    <ErrorMessage class="text-red-500 text-xs italic" name="email"/>
                </div>
    
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="password">Password</label>
                    <Field type="password"
                        name="password"
                        placeholder="Enter your password"
                        class="w-full px-3 py-2 border rounded-md shadow-sm focus:outline-none focus:border-blue-500 focus:ring focus:ring-blue-500"
                        :rules="validatePassword"
                        v-model="state.user.password"
                    />
                    <ErrorMessage class="text-red-500 text-xs italic" name="password"/>
                </div>
    
                <button type="submit" class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                    Login
                </button>
            </Form>
            <p class="text-blue-500 text-sm italic mt-8 text-center"><NuxtLink href="/register">Create an Account</NuxtLink></p>
        </div>
    </div>
</template>
  
<script setup>
    definePageMeta({
        layout: 'form'
    });

    import { Form, Field, ErrorMessage } from 'vee-validate';

    const validateEmail = (value) => {
        // if the field is empty
        if (!value) {
        return 'This field is required';
        }
        // if the field is not a valid email
        const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
        if (!regex.test(value)) {
        return 'This field must be a valid email';
        }
        return true;
    };

    const validatePassword = (value) => {
        // if the field is empty
        if (!value) {
        return 'This field is required';
        }
        return true;
    };

    const state = reactive({
        errors: null,
        user: {
        email: null,
        password: null,
        }
    });
  
    async function handleLogin() {
        const params = {
        email: state.user.email,
        password: state.user.password,
        }
    
        try {
        const response = await $fetch(`http://127.0.0.1:8000/api/auth/login`, {
            method: 'POST',
            body: JSON.stringify(params)
        });
    
        if (response.data) {
            localStorage.setItem('_token', response.data.token);
            navigateTo('/dashboard');
        }
        } catch (error) {
        state.errors = error.response;
        alert(state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.email && state.errors._data.errors.email[0]);
        }
    }
</script>

