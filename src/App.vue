<script setup>
import Window from './components/Window.vue';
import TaskBar from './components/TaskBar.vue';
</script>

<template>
  <header>
  </header>
  <main>
    <Window />
  </main>
  <footer>
    <TaskBar />
  </footer>
</template>

<style >
  body {
    zoom: 1.5;
    background-color: rgb(54, 123, 123);
    margin: 0;
    padding: 0;
  }

  main {
    height: 60vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  footer {
    position: fixed;
    bottom: 0;
    width: 100%;
  }
</style>
