<script setup>
import Window from './components/Window.vue';
import TaskBar from './components/TaskBar.vue';
import Desktop from './components/Desktop.vue';
import Browser from './components/Browser.vue';
import Homepage from './components/Homepage.vue';
</script>

<template>
  <main>
    <Desktop>
      <Window>
        <Browser>
          <Homepage />
        </Browser>
      </Window>
    </Desktop>
    <TaskBar />
  </main>
</template>
