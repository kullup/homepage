<template>
    <div class="window">
        <div class="window-body">
            <div class="programm-list" >
                <button>About</button>
                <button>Contact</button>
            </div>
            <div class="status-bar ">
                <p class="status-bar-field">16:37</p>
            </div>
        </div>
  </div>
</template>

<style scoped>
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
</style>