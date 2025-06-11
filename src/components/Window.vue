<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const windowRef = ref(null)
const isDragging = ref(false)
const dragStart = ref({ x: 0, y: 0 })
const windowPosition = ref({ x: 0, y: 0 })
const isMaximized = ref(true) // Start maximized
const originalPosition = ref({ x: 0, y: 0 })
let animationFrameId = null

const startDrag = (event) => {
  // Don't allow dragging when maximized
  if (isMaximized.value) return

  isDragging.value = true
  // Account for the zoom factor (1.5 from App.vue)
  const zoomFactor = 1.5
  const clientX = event.clientX / zoomFactor
  const clientY = event.clientY / zoomFactor

  dragStart.value = {
    x: clientX - windowPosition.value.x,
    y: clientY - windowPosition.value.y
  }
  event.preventDefault()

  // Add visual feedback for dragging
  if (windowRef.value) {
    windowRef.value.style.willChange = 'transform'
  }
}

const drag = (event) => {
  if (!isDragging.value) return

  // Cancel previous animation frame if it exists
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
  }

  // Use requestAnimationFrame for smooth updates
  animationFrameId = requestAnimationFrame(() => {
    // Account for the zoom factor (1.5 from App.vue)
    const zoomFactor = 1.5
    const clientX = event.clientX / zoomFactor
    const clientY = event.clientY / zoomFactor

    windowPosition.value = {
      x: clientX - dragStart.value.x,
      y: clientY - dragStart.value.y
    }
  })
}

const stopDrag = () => {
  isDragging.value = false

  // Clean up animation frame and will-change hint
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
    animationFrameId = null
  }

  if (windowRef.value) {
    windowRef.value.style.willChange = 'auto'
  }
}

const toggleMaximize = () => {
  if (isMaximized.value) {
    // Restore window
    isMaximized.value = false
    windowPosition.value = { ...originalPosition.value }
  } else {
    // Save current position and maximize
    originalPosition.value = { ...windowPosition.value }
    isMaximized.value = true
    windowPosition.value = { x: 0, y: 0 }
  }
}

onMounted(() => {
  document.addEventListener('mousemove', drag)
  document.addEventListener('mouseup', stopDrag)
})

onUnmounted(() => {
  document.removeEventListener('mousemove', drag)
  document.removeEventListener('mouseup', stopDrag)
})
</script>

<template>
  <div ref="windowRef" class="window" :class="{ maximized: isMaximized }" :style="{
    transform: `translate3d(${windowPosition.x}px, ${windowPosition.y}px, 0)`
  }">
    <div class="title-bar" @mousedown="startDrag">
      <div class="title-bar-text">A Window</div>
      <div class="title-bar-controls">
        <button aria-label="Minimize"></button>
        <button aria-label="Maximize" @click="toggleMaximize"></button>
        <button aria-label="Close"></button>
      </div>
    </div>

    <slot></slot>
  </div>
</template>

<style scoped>
.window {
  width: 80%;
  height: 80%;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: absolute;
  z-index: 1;
}

.window.maximized {
  width: 100%;
  height: 100%;
  transform: translate3d(0, 0, 0) !important;
  position: static;
}

.title-bar {
  cursor: move;
  user-select: none;
}

.window.maximized .title-bar {
  cursor: default;
}

.window-body {
  margin: 2px 0 0 0;
  height: 100%;
  background-color: rgb(255, 255, 255);
}
</style>