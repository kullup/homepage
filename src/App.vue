<script setup>
import Window from './components/Window.vue';
import TaskBar from './components/TaskBar.vue';
</script>

<template>
  <main>
    <div class="desktop">
      <Window />
    </div>
    <TaskBar />
  </main>
</template>

<style >
  .desktop {
    background-color: rgb(54, 123, 123);
    flex: 1;
  }

  main {
    display: flex;
    flex-direction: column;
    height: 100vh;
    width: 100vw;
  }

  body {
    margin: 0;
    padding: 0;
  }
</style>
