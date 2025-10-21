<template>
    <div class="field-row">
        <label for="text17">Address</label>
        <input id="text17" type="text" value="https://jon-schulte.com/index.php" />
    </div>
    <div class="sunken-panel">
        <slot></slot>
    </div>
</template>

<style scoped>
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
</style>