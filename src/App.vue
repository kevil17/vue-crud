<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>

    <div class="wrapper"  >
      <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <RouterLink class="navbar-brand" to="/">NavBar</RouterLink>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <RouterLink class="nav-link" aria-current="page" to="/">Home</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" aria-current="page" to="/about">About Us</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" aria-current="page" to="/users">Users</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" aria-current="page" to="/users/create">Create Users</RouterLink>
        </li>
      </ul>
    </div>
  </div>
</nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
</style>
