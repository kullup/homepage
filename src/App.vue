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
    width: 100%;
    max-height: calc(100% - 33px);
    max-width: calc(100% - 6px);
    padding-right: 6px;
    display: flex;
    flex-direction: column;
  }

  main {
    height: 66.66666vh;
    width: 66.66666vw;
    background-color: rgb(231, 231, 231);
    display: flex;
    flex-direction: column;
    zoom: 1.5;
  }

  body {
    overflow: hidden;
    margin: 0;
    padding: 0;
  }
</style>
