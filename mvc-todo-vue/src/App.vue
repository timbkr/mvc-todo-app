<script setup lang="ts">
import ToDoList from './components/ToDoList.vue';
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    <div class="row container heading">
      <h1>ToDo-App</h1>
      <img src="./assets/icons/icon-sun.svg" alt="">
      <!-- <img src="../assets/icons/icon-sun.svg" alt=""> -->
      <!-- <img src="../public/assets/icons/icon-moon.svg" alt=""> -->
    </div>

  </header>

  <main>
    <ToDoList />
  </main>
</template>

<style scoped>
.heading{
  justify-content: space-between;
}
</style>
