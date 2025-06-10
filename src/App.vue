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
    height: 100%;
    max-height: 92.6%;
    display: flex;
    flex-direction: column;
  }

  main {
    overflow: hidden;
    height: 66.66666vh;
    width: 66.66666vw;
    background-color: rgb(231, 231, 231);
    display: flex;
    flex-direction: column;
    zoom: 1.3;
  }

  body {
    margin: 0;
    padding: 0;
  }
</style>
