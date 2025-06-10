<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const windowRef = ref(null)
const isDragging = ref(false)
const dragStart = ref({ x: 0, y: 0 })
const windowPosition = ref({ x: 50, y: 50 })
let animationFrameId = null

const startDrag = (event) => {
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
    <div 
        ref="windowRef"
        class="window" 
        :style="{ 
            transform: `translate3d(${windowPosition.x}px, ${windowPosition.y}px, 0)`,
            position: 'absolute'
        }"
    >
        <div class="title-bar" @mousedown="startDrag">
            <div class="title-bar-text">A Window</div>
            <div class="title-bar-controls">
            <button aria-label="Minimize"></button>
            <button aria-label="Maximize"></button>
            <button aria-label="Close"></button>
            </div>
        </div>
        <div class="field-row">
            <label for="text17">Address</label>
            <input id="text17" type="text" value="https://jon300.cool" />
        </div>
        <div class="sunken-panel">
            <p>
                The quick brown fox jumps over the lazy dog. This is a classic pangram used to test fonts and keyboards.
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
            </p>
            <img src="../assets/php.png" alt="Word Art" class="img php">
            <p>
                PHP is a popular general-purpose scripting language that is especially suited to web development. Fast, flexible and pragmatic, PHP powers everything from your blog to the most popular websites in the world.
            </p>
            <img src="../assets/wordart.png" alt="Word Art" class="img">
            <p>
                This is a simple text paragraph to demonstrate the layout of the window. It contains multiple lines of text to show how the content flows within the window.
                You can add more text here to see how it behaves with different lengths and styles.
            </p>   
            <p>
                Another paragraph to further illustrate the text wrapping and layout capabilities of this window component. Feel free to modify the content as needed.
            </p>
            <p>
                This is the last paragraph in this example. It serves to show how the text appears at the bottom of the window, ensuring that everything fits nicely within the defined space.
            </p>
        </div>
    </div>
</template>

<style scoped>
    .window {
        width: 200px; /* fullscreen: width: full */
        height: 300px; /* fullscreen: height: 100% */
        display: flex;
        flex-direction: column;
        overflow: hidden;
        position: absolute;
        z-index: 1;
    }

    .title-bar {
        cursor: move;
        user-select: none;
    }

    .window-body {
        margin: 2px 0 0 0;
        height: 100%;
        background-color: rgb(255, 255, 255);
    }

    .sunken-panel {
        margin: 2px 0 0 0;
        height: 100%;
        background-color: rgb(219, 240, 239);
    }

    .field-row {
        margin: 2px 0px 0px 2px;
    }

    input {
        width: 100%;
    }

    p {
        padding: 0 10px 0 10px;
        font-size: 12px;
        line-height: 1.2;
    }

    .img {
        width: 100%;
        max-width: 400px;
        height: auto;
    }

    .php {
        width: 100px;
        padding: 10px 0 10px 0;
        animation: rotate 15s linear infinite;
    }

    @keyframes rotate {
        from {
            transform: rotate(0deg);
        }
        to {
            transform: rotate(360deg);
        }
    }
</style>