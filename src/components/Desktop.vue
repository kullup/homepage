<template>
    <div class="desktop">
        <slot></slot>
    </div>
</template>

<style >
  .desktop {
    background-color: rgb(54, 123, 123);
    height: 100%;
    width: 100%;
    max-height: calc(100% - 33px);
    max-width: calc(100% - 6px);
    padding-right: 6px;
    position: relative;
  }
</style>
