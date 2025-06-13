<template>
    <div class="monitor">
        <div class="screen-outer-border">
            <div class="screen-inner-border">
                <div class="screen">
                    <slot></slot>
                </div>
            </div>
        </div>
        <div class="monitor-controls">
            <div class="green led"></div>
            <div class="orange led"></div>
        </div>
    </div>
</template>

<style scoped>
.led {
    width: 6px;
    height: 6px;
    border-radius: 50%;
}

.orange {
    background-color: rgb(220, 135, 44);
    box-shadow: 0 0 5px rgba(228, 214, 17, 0.5);
}

.green {
    background-color: rgb(44, 220, 44);
    box-shadow: 0 0 5px rgba(17, 228, 17, 0.5);
}

.monitor-controls {
    /* box-shadow: inset 0 0 4px rgba(0, 0, 0, 0.6); */
    border: 0px;
    /* border-color: rgba(0, 0, 0, 0.462); */
    border-style: solid;
    border-radius: 0px;
    color: white;
    height: 28px;
    font-size: 14px;
    z-index: 101; /* Ensure controls are above the screen */
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 12px;
}

.screen-outer-border {
    border-style: solid;
    border-top-color: rgb(207, 208, 198);
    border-right-color: rgb(225, 226, 216);
    border-bottom-color: rgb(207, 208, 198);
    border-left-color: rgb(225, 226, 216);
    background-color: rgb(207, 208, 198);;
    border-width: 8px 8px 8px 8px;
    border-radius: 8px;
    width: 100%;
    flex: 1;
    box-sizing: border-box;
    position: relative;
}

.screen-inner-border {
    border-width: 0.2em 0.2em 0.2em 0.2em;
    border-style: solid;
    border-color: rgb(0, 0, 0);
    background-color: rgb(0, 0, 0);
    border-radius: 5px;
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    position: relative;
}

.monitor {
    height: 66.66666dvh;
    width: 66.66666dvw;
    border-style: solid;
    border-color: rgb(249, 250, 232);
    border-width: 16px 16px 0px 16px;
    background-color: rgb(249, 250, 232);
    position: relative;
    scale: 1.5;
    transform-origin: top left;
    top: 0;
    left: 0;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
}

.screen {
    height: 100%;
    width: 100%;
    background-color: rgb(0, 0, 0);
    display: flex;
    flex-direction: column;
    position: absolute;
    overflow: hidden;
    filter: brightness(0.93) contrast(1.3) saturate(1) hue-rotate(10deg);
}

/* Vignette effect for old monitor simulation */
.screen::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(ellipse at center, transparent 50%, rgba(0, 0, 0, 0.15)85%, rgba(0, 0, 0, 0.4) 100%);
    pointer-events: none;
    z-index: 99999;
}

/* CRT overlay covering the main element */
.screen::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: url('../assets/crt-overlay-frame.png');
    background-size: 100% 100%;
    background-repeat: no-repeat;
    background-position: center;
    pointer-events: none;
    z-index: 100000;
    mix-blend-mode: overlay;
    opacity: 0.5;
}
</style>