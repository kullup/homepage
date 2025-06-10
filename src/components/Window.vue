<template>
    <div class="window">
        <div class="title-bar">
            <div class="title-bar-text">A Window</div>
            <div class="title-bar-controls">
            <button aria-label="Minimize"></button>
            <button aria-label="Maximize"></button>
            <button aria-label="Close"></button>
            </div>
        </div>
        <div class="window-body">
            hu
        </div>
    </div>
</template>

<style scoped>
    .window {
        width: full;
        height: 100%;
        display: flex;
        flex-direction: column;
    }

    .window-body {
        margin: 2px 0 0 0;
        height: 100%;
        background-color: rgb(255, 255, 255);
    }

    .sunken-panel {
        overflow-y: auto;
        max-height: calc(66.6666vh - 61px);
    }

    .wordart {
        width: 100%;
        max-width: 400px;
        height: auto;
        margin-top: 20px;
    }

    p {
        padding: 0 10px 0 10px;
        font-size: 12px;
        line-height: 1.2;
    }
</style>