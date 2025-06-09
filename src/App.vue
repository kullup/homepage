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
  body {
    zoom: 1.5;
    overflow: hidden;
  }

  .desktop {
    background-color: rgb(54, 123, 123);
    height: 100%;
  }

  main {
    display: flex;
    flex-direction: column;
    height: 66.66666vh;
    width: 66.66666vw;
  }

  body {
    margin: 0;
    padding: 0;
  }
</style>
