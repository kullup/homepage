<script setup>
import { ref } from 'vue';
import Window from './components/Window.vue';
import TaskBar from './components/TaskBar.vue';
import Desktop from './components/Desktop.vue';
import Browser from './components/Browser.vue';
import Homepage from './components/Homepage.vue';
import Monitor from './components/Monitor.vue';

const windows = ref([
  { id: 'browser', title: 'Browser', zIndex: 2, initialX: 0, initialY: 0 },
  { id: 'contact', title: 'Contact', zIndex: 1, initialX: 50, initialY: 50 }
]);

const activeWindow = ref('browser');

const bringToFront = (id) => {
  activeWindow.value = id;
  const maxZIndex = Math.max(...windows.value.map(w => w.zIndex));
  const window = windows.value.find(w => w.id === id);
  if (window) {
    window.zIndex = maxZIndex + 1;
  }
};
</script>

<template>
  <main>
    <Monitor>
      <Desktop>
        <Window
          v-for="window in windows"
          :key="window.id"
          :title="window.title"
          :initial-x="window.initialX"
          :initial-y="window.initialY"
          :z-index="window.zIndex"
          @focus="bringToFront(window.id)"
        >
          <Browser v-if="window.id === 'browser'">
            <Homepage />
          </Browser>
          <div v-if="window.id === 'contact'" class="field-row-stacked" style="width: 200px">
            <label for="text18">Address (Line 1)</label>
            <input id="text18" type="text" />
            <label for="text19">Address (Line 2)</label>
            <input id="text19" type="text" />
          </div>
        </Window>
      </Desktop>
      <TaskBar :windows="windows" :active-window="activeWindow" @select-window="bringToFront" />
    </Monitor>
  </main>
</template>
