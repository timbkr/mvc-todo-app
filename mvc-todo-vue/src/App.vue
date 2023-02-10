<script setup lang="ts">
import ToDoList from './components/ToDoList.vue';
</script>

<script lang="ts">
export default{
  data(){
    return{
      isDarkModeActive: false
    }
  },
  methods:{
    toggleDarkMode(){
      this.isDarkModeActive = !this.isDarkModeActive
      this.setLocalStorage();
      if(this.isDarkModeActive)
        document.body.classList.add('lightMode')
      else document.body.classList.remove('lightMode')
    },
    getLocalStorage(){
      const darkMode = localStorage.getItem('darkMode');
      if(darkMode === 'enabled') return true
      else if(darkMode === 'disabled') return false
      return this.isDarkModeActive
    },
    setLocalStorage(){
      if(this.isDarkModeActive) localStorage.setItem('darkMode','enabled')
      else localStorage.setItem('darkMode','disabled')
    }
  },
  mounted(){
    //set Light / Darkmode to saved mode
    if(this.getLocalStorage() !== this.isDarkModeActive) this.toggleDarkMode();
  }
}
</script>
<template>
  <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->
  <header>
    <div class="row container heading">
      <h1>ToDo-App</h1>
      <img v-if="!isDarkModeActive" src="./assets/icons/icon-sun.svg" alt="" @click="toggleDarkMode">
      <img v-if="isDarkModeActive" src="./assets/icons/icon-moon.svg" alt="" @click="toggleDarkMode">
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
  align-items: center;
}
.heading img{
  height: 100%;
  cursor: pointer;
}
.heading img:hover{
  opacity: 0.75;
}

.logo{
  margin: 0 auto;
  width: 20%;
  height: auto;
}
</style>
