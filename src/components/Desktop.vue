<template>
    <div class="desktop">
        <slot></slot>
    </div>
</template>

<style >
  .desktop {
    background-color: rgb(54, 123, 123);
    height: 180%;
    width: 100%;
    max-height: 100%;
    max-width: 100%;
    position: relative;
    overflow: hidden;
  }
</style>
