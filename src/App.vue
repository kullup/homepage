<script setup>
import Window from './components/Window.vue';
import TaskBar from './components/TaskBar.vue';
import Desktop from './components/Desktop.vue';
import Browser from './components/Browser.vue';
import Homepage from './components/Homepage.vue';
import Monitor from './components/Monitor.vue';
</script>

<template>
  <main>
    <Monitor>
      <Desktop>
        <Window>
          <Browser>
            <Homepage />
          </Browser>
        </Window>
      </Desktop>
      <TaskBar />
    </Monitor>
  </main>
</template>
