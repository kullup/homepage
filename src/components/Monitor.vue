<template>
    <div class="monitor">
        <div class="screen-inner-border">
            <div class="screen">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<style scoped>

.screen-inner-border {
    border: 1px solid rgb(0, 0, 0);
    border-radius: 5px;
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    position: relative;
    overflow: hidden;
}

.monitor {
    height: 66.66666dvh;
    width: 66.66666dvw;
    border: 30px solid rgb(249, 250, 232);
    border-radius: 20px;
    position: relative;
    scale: 1.5;
    transform-origin: top left;
    top: 0;
    left: 0;
    box-sizing: border-box;
}

.screen {
    height: 100%;
    width: 100%;
    background-color: rgb(157, 156, 133);
    display: flex;
    flex-direction: column;
    scale: 1.0;
    position: absolute;
    top: 0;
    left: 0;
    transform-origin: top left;
    filter: brightness(1.03) contrast(1.05);
}

/* Vignette effect for old monitor simulation */
.screen::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(ellipse at center, transparent 50%, rgba(0, 0, 0, 0.15)90%, rgba(0, 0, 0, 0.4) 100%);
    pointer-events: none;
    z-index: 99;
}

/* CRT overlay covering the main element */
.screen::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: url('../assets/crt-overlay.png');
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    pointer-events: none;
    z-index: 100;
    mix-blend-mode: overlay;
    opacity: 0.2;
}
</style>