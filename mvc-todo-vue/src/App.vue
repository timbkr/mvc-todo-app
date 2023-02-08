<script setup lang="ts">
import ToDoList from './components/ToDoList.vue';
</script>

<template>
  <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
  <header>
    <div class="row container heading">
      <h1>ToDo-App</h1>
      <img src="./assets/icons/icon-sun.svg" alt="">
      <!-- <img src="./assets/icons/icon-sun.svg" alt=""> -->
    </div>

  </header>

  <main>
    <div class="container">
      <ToDoList />

    </div>
  </main>
</template>

<style scoped>
.heading {
  justify-content: space-between;
  padding: 2em 0;
}
</style>
