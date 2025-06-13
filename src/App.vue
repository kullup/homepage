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
        <Window title="Browser" :initial-x="0" :initial-y="0" :initial-z-index="2">
          <Browser>
            <Homepage />
          </Browser>
        </Window>
        <Window title="Empty Window" :initial-x="50" :initial-y="50" :initial-z-index="1">
          
        </Window>
      </Desktop>
      <TaskBar />
    </Monitor>
  </main>
</template>
