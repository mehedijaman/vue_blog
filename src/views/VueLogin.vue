<script setup>
import { ref } from 'vue';

const user = {
    name:'Mehedi Jaman',
    username:'mehedi',
    password:'123',
    email:'mail4mjaman@gmail.com'
}

const username = ref('');
const password = ref('');

function login() {
    if(username.value == user.username && password.value == user.password){
        router.push({
            name: 'LandingPage',
            query: { 
                name: user.name, 
                username: user.username, 
                email: user.email
            },
        });
    }
</script>

<template>
  <div>
    <form @submit.prevent="login()">
      <label for="username">Username/Email:</label>
      <input v-model="username" type="text" id="username" required />

      <label for="password">Password:</label>
      <input v-model="password" type="password" id="password" required />

      <button type="submit">Login</button>
    </form>
  </div>
</template>

