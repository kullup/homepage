<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  initialX: { type: Number, default: 0 },
  initialY: { type: Number, default: 0 },
  initialWidth: { type: Number, default: 640 },
  initialHeight: { type: Number, default: 480 },
  zIndex: { type: Number, default: 1 },
  title: { type: String, default: 'A Window' },
  isMinimized: { type: Boolean, default: false },
  initialMaximized: { type: Boolean, default: false },
  disableMaximize: { type: Boolean, default: false },
  forceMaximized: { type: Boolean, default: false }
})

const emit = defineEmits(['focus', 'minimize', 'close'])

const windowRef = ref(null)
const isDragging = ref(false)
const isResizing = ref(false)
const dragStart = ref({ x: 0, y: 0 })
const resizeStart = ref({ x: 0, y: 0, width: 0, height: 0 })
const windowPosition = ref({ x: props.initialX, y: props.initialY })
const windowSize = ref({ width: props.initialWidth, height: props.initialHeight })
const isMaximized = ref(props.initialMaximized)
const isActuallyMaximized = computed(() => isMaximized.value || props.forceMaximized)
const originalPosition = ref({ x: props.initialX, y: props.initialY })
const originalSize = ref({ width: props.initialWidth, height: props.initialHeight })
let animationFrameId = null

const startDrag = (event) => {
  if (isActuallyMaximized.value) return

  emit('focus')

  isDragging.value = true
  const zoomFactor = 1.5
  const clientX = event.clientX / zoomFactor
  const clientY = event.clientY / zoomFactor

  dragStart.value = {
    x: clientX - windowPosition.value.x,
    y: clientY - windowPosition.value.y
  }
  event.preventDefault()

  if (windowRef.value) {
    windowRef.value.style.willChange = 'transform'
  }
}

const drag = (event) => {
  if (!isDragging.value) return

  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
  }

  animationFrameId = requestAnimationFrame(() => {
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

  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
    animationFrameId = null
  }

  if (windowRef.value) {
    windowRef.value.style.willChange = 'auto'
  }
}

const startResize = (event) => {
  if (isActuallyMaximized.value) return

  emit('focus')
  isResizing.value = true
  const zoomFactor = 1.5
  const clientX = event.clientX / zoomFactor
  const clientY = event.clientY / zoomFactor

  resizeStart.value = {
    x: clientX,
    y: clientY,
    width: windowSize.value.width,
    height: windowSize.value.height
  }
  event.preventDefault()

  if (windowRef.value) {
    windowRef.value.style.willChange = 'width, height'
  }
}

const resize = (event) => {
  if (!isResizing.value) return

  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
  }

  animationFrameId = requestAnimationFrame(() => {
    const zoomFactor = 1.5
    const clientX = event.clientX / zoomFactor
    const clientY = event.clientY / zoomFactor

    const deltaX = clientX - resizeStart.value.x
    const deltaY = clientY - resizeStart.value.y

    const minWidth = 320
    const minHeight = 240

    const nextWidth = Math.max(minWidth, resizeStart.value.width + deltaX)
    const nextHeight = Math.max(minHeight, resizeStart.value.height + deltaY)

    windowSize.value = { width: nextWidth, height: nextHeight }
  })
}

const stopResize = () => {
  isResizing.value = false

  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
    animationFrameId = null
  }

  if (windowRef.value) {
    windowRef.value.style.willChange = 'auto'
  }
}

const toggleMaximize = () => {
  if (props.disableMaximize || props.forceMaximized) return
  if (isMaximized.value) {
    isMaximized.value = false
    windowPosition.value = { ...originalPosition.value }
    windowSize.value = { ...originalSize.value }
  } else {
    originalPosition.value = { ...windowPosition.value }
    originalSize.value = { ...windowSize.value }
    isMaximized.value = true
    windowPosition.value = { x: 0, y: 0 }
    emit('focus')
  }
}

const minimize = () => {
  emit('minimize')
}

onMounted(() => {
  document.addEventListener('mousemove', drag)
  document.addEventListener('mouseup', stopDrag)
  document.addEventListener('mousemove', resize)
  document.addEventListener('mouseup', stopResize)
})

onUnmounted(() => {
  document.removeEventListener('mousemove', drag)
  document.removeEventListener('mouseup', stopDrag)
  document.removeEventListener('mousemove', resize)
  document.removeEventListener('mouseup', stopResize)
})
</script>

<template>
  <div v-if="!isMinimized" ref="windowRef" class="window" :class="{ maximized: isActuallyMaximized }" :style="{
    transform: `translate3d(${windowPosition.x}px, ${windowPosition.y}px, 0)`,
    zIndex: props.zIndex,
    width: isActuallyMaximized ? '100%' : windowSize.width + 'px',
    height: isActuallyMaximized ? '100%' : windowSize.height + 'px'
  }" @mousedown.left="$emit('focus')">
    <div class="title-bar" @mousedown.left.stop="startDrag">
      <div class="title-bar-text">{{ title }}</div>
      <div class="title-bar-controls">
        <button aria-label="Minimize" @click="minimize"></button>
        <button v-if="!disableMaximize" aria-label="Maximize" @click="toggleMaximize"></button>
        <button aria-label="Close" @click="$emit('close')"></button>
      </div>
    </div>

    <slot></slot>

    <div v-if="!isActuallyMaximized" class="resize-handle br" @mousedown.left.stop="startResize"></div>
  </div>
</template>

<style scoped>
.window {
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: absolute;
  z-index: 1;
  box-sizing: border-box;
}

.window.maximized {
  width: 100%;
  height: 100%;
  transform: translate3d(0, 0, 0) !important;
  position: absolute;
  top: 0;
  left: 0;
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

.resize-handle.br {
  position: absolute;
  width: 14px;
  height: 14px;
  right: 0;
  bottom: 0;
  cursor: nwse-resize;
  background: transparent;
}
</style>