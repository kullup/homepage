<script setup>
import worldIcon from '../assets/world.png';
import mailIcon from '../assets/mail.png';

const props = defineProps({
    windows: { type: Array, required: true },
    activeWindow: { type: String, required: true }
});

const emit = defineEmits(['select-window']);

const getIcon = (title) => {
    switch (title) {
        case 'Browser':
            return worldIcon;
        case 'Contact':
            return mailIcon;
        default:
            return '';
    }
};

const selectWindow = (id) => {
  emit('select-window', id)
}
</script>

<template>
    <div class="window">
        <div class="window-body">
            <div class="programm-list">
                <button v-for="window in windows" :key="window.id" :class="{ active: window.id === activeWindow }"
                    @click="selectWindow(window.id)">
                    <img :src="getIcon(window.title)" :alt="window.title" class="button-icon">
                    {{ window.title }}
                </button>
            </div>
            <div class="status-bar ">
                <p class="status-bar-field">16:37</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.window {
    width: full;
    z-index: 10;
}

.window-body {
    margin: 2px;
    display: flex;
    justify-content: space-between;
}

.status-bar-field {
    padding: 5px;
}

.start-button {
    padding: 0 10px 0 10px;
    min-width: 0px;
}

.programm-list {
    display: flex;
    align-items: center;
    gap: 5px;
}

.programm-list button {
    display: flex;
    align-items: center;
}

.button-icon {
    width: 15px;
    height: 15px;
    margin-right: 8px;
}

.active {
    box-shadow: inset -1px -1px #ffffff, inset 1px 1px #0a0a0a,
        inset -2px -2px #dfdfdf, inset 2px 2px #808080;
}

button {
    min-width: 0px;
    padding-inline-start: 4px;
}
</style>