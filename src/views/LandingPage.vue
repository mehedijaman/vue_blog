<script setup>

</script>
<template>
    <div>
      <h2>Welcome to the Landing Page</h2>
      <p>Name: {{ $route.query.name }}</p>
      <p>Username: {{ $route.query.username }}</p>
      <p>Email: {{ $route.query.email }}</p>
    </div>
  </template>
  
  