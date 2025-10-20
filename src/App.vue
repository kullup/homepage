<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import Window from './components/Window.vue';
import TaskBar from './components/TaskBar.vue';
import Desktop from './components/Desktop.vue';
import Browser from './components/Browser.vue';
import Homepage from './components/Homepage.vue';
import Contact from './components/Contact.vue';
import Monitor from './components/Monitor.vue';

const activeWindow = ref('browser');

// Track whether viewport is mobile (≤768px) — set synchronously for initial render
const isMobile = ref(
  typeof window !== 'undefined' && typeof window.matchMedia === 'function'
    ? window.matchMedia('(max-width: 768px)').matches
    : false
);

// Keep these in sync with the props passed to <Window>
const WINDOW_WIDTH = 400;
const WINDOW_HEIGHT = 350;

// Pre-center the browser window on desktop before first render
const monitorScaleFactor = 1.5; // must match Monitor.vue CSS scale and Window drag zoomFactor
const centerBrowserPosition = () => {
  if (typeof window === 'undefined') return { x: 0, y: 0 };

  // Convert viewport to pre-scale space used by Window positioning
  const preScaleViewportWidth = window.innerWidth / monitorScaleFactor;
  const preScaleViewportHeight = window.innerHeight / monitorScaleFactor;

  // Account for monitor and screen borders and the monitor controls area
  // Monitor borders (px): left+right are 40px on wide screens, 8px on <=1024px
  const narrow = typeof window.matchMedia === 'function' && window.matchMedia('(max-width: 1024px)').matches;
  const monitorHorizontalBorder = narrow ? (8 + 8) : (40 + 40);
  const monitorVerticalBorder = 8 + 0; // top + bottom

  // Screen border wrappers
  const screenOuterBorderH = 8 + 8; // .screen-outer-border left+right
  const screenOuterBorderV = 8 + 8; // top+bottom
  const screenInnerBorderH = 3.2 + 3.2; // 0.2em each side (assuming 16px base)
  const screenInnerBorderV = 3.2 + 3.2;
  const monitorControlsHeight = 28; // height of controls below the screen

  const screenContentWidth = preScaleViewportWidth - monitorHorizontalBorder - screenOuterBorderH - screenInnerBorderH;
  const screenContentHeight = preScaleViewportHeight - monitorVerticalBorder - screenOuterBorderV - screenInnerBorderV - monitorControlsHeight;

  const x = Math.max(0, Math.floor((screenContentWidth - WINDOW_WIDTH) / 2));
  const y = Math.max(0, Math.floor((screenContentHeight - WINDOW_HEIGHT) / 2)) - 16;
  return { x, y };
};

const initialBrowserPosition = isMobile.value ? { x: 0, y: 0 } : centerBrowserPosition();

const windows = ref([
  { id: 'browser', title: 'Browser', zIndex: 2, initialX: initialBrowserPosition.x, initialY: initialBrowserPosition.y, isMinimized: false },
  { id: 'contact', title: 'Contact', zIndex: 1, initialX: 50, initialY: 50, isMinimized: false }
]);

// Easy accessors for window configs used in the template
const browserWindow = computed(() => windows.value.find(w => w.id === 'browser'));
const contactWindow = computed(() => windows.value.find(w => w.id === 'contact'));

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
  // disable that feature for now, looks nicer this way
  // if (isMobile.value) {
  if (true) {
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
        <!-- Browser Window -->
        <Window
          :title="browserWindow.title"
          :initial-x="browserWindow.initialX"
          :initial-y="browserWindow.initialY"
          :initial-width="WINDOW_WIDTH"
          :initial-height="WINDOW_HEIGHT"
          :z-index="browserWindow.zIndex"
          :initial-maximized="isMobile"
          :disable-maximize="isMobile"
          :force-maximized="isMobile"
          :is-minimized="browserWindow.isMinimized"
          @focus="bringToFront('browser')"
          @minimize="toggleMinimize('browser')"
          @close="closeWindow('browser')"
        >
          <Browser>
            <Homepage />
          </Browser>
        </Window>

        <!-- Contact Window -->
        <Window
          :title="contactWindow.title"
          :initial-x="contactWindow.initialX"
          :initial-y="contactWindow.initialY"
          :initial-width="WINDOW_WIDTH / 2"
          :initial-height="WINDOW_HEIGHT / 2"
          :z-index="contactWindow.zIndex"
          :initial-maximized="isMobile"
          :disable-maximize="isMobile"
          :force-maximized="isMobile"
          :is-minimized="contactWindow.isMinimized"
          @focus="bringToFront('contact')"
          @minimize="toggleMinimize('contact')"
          @close="closeWindow('contact')"
        >
          <Contact />
        </Window>
      </Desktop>

      <TaskBar :windows="windows" :active-window="activeWindow" @select-window="bringToFront" />
    </Monitor>
  </main>
</template>
