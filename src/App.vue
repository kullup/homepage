<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import Window from './components/Window.vue';
import TaskBar from './components/TaskBar.vue';
import Desktop from './components/Desktop.vue';
import Browser from './components/Browser.vue';
import Homepage from './components/Homepage.vue';
import Monitor from './components/Monitor.vue';

const windows = ref([
  { id: 'browser', title: 'Browser', zIndex: 2, initialX: 0, initialY: 0, isMinimized: false },
  { id: 'contact', title: 'Contact', zIndex: 1, initialX: 50, initialY: 50, isMinimized: false }
]);

const activeWindow = ref('browser');

// Track whether viewport is mobile (≤768px) — set synchronously for initial render
const isMobile = ref(
  typeof window !== 'undefined' && typeof window.matchMedia === 'function'
    ? window.matchMedia('(max-width: 768px)').matches
    : false
);

const evaluateViewport = () => {
  if (typeof window !== 'undefined' && typeof window.matchMedia === 'function') {
    isMobile.value = window.matchMedia('(max-width: 768px)').matches;
  } else {
    isMobile.value = false;
  }
};

onMounted(() => {
  evaluateViewport();

  // Initialize window states for mobile once on load
  if (isMobile.value) {
    windows.value.forEach(w => {
      w.isMinimized = w.id !== 'browser';
    });
    activeWindow.value = 'browser';
  }

  // Optional: keep `isMobile` reactive on viewport changes
  let mql = null;
  if (typeof window !== 'undefined' && typeof window.matchMedia === 'function') {
    mql = window.matchMedia('(max-width: 768px)');
    const handler = (e) => { isMobile.value = e.matches; };
    // Newer browsers: addEventListener; fallback to addListener
    if (typeof mql.addEventListener === 'function') {
      mql.addEventListener('change', handler);
      onUnmounted(() => mql.removeEventListener('change', handler));
    } else if (typeof mql.addListener === 'function') {
      mql.addListener(handler);
      onUnmounted(() => mql.removeListener(handler));
    }
  }
});

const bringToFront = (id) => {
  activeWindow.value = id;
  const maxZIndex = Math.max(...windows.value.map(w => w.zIndex));
  const window = windows.value.find(w => w.id === id);
  if (window) {
    window.zIndex = maxZIndex + 1;
    window.isMinimized = false;
  }
};

const toggleMinimize = (id) => {
  const window = windows.value.find(w => w.id === id);
  if (window) {
    window.isMinimized = !window.isMinimized;
    if (window.isMinimized && activeWindow.value === id) {
      const nextActiveWindow = windows.value.filter(w => !w.isMinimized).sort((a, b) => b.zIndex - a.zIndex)[0];
      activeWindow.value = nextActiveWindow ? nextActiveWindow.id : '';
    }
  }
};

const closeWindow = (id) => {
  toggleMinimize(id);
};
</script>

<template>
  <main>
    <Monitor>
      <Desktop>
        <Window
          v-for="window in windows.filter(w => !w.isMinimized)"
          :key="window.id"
          :title="window.title"
          :initial-x="window.initialX"
          :initial-y="window.initialY"
          :initial-width="400"
          :initial-height="300"
          :z-index="window.zIndex"
          :initial-maximized="isMobile && window.id === 'browser'"
          :is-minimized="window.isMinimized"
          @focus="bringToFront(window.id)"
          @minimize="toggleMinimize(window.id)"
          @close="closeWindow(window.id)"
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
