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
        <div class="sunken-panel">
            The quick brown fox jumps over the lazy dog. This is a classic pangram used to test fonts and keyboards.
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
            Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
            <img src="../assets/wordart.png" alt="Word Art" class="wordart">
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
        width: full;
        height: 100%;
        display: flex;
        flex-direction: column;
        overflow: hidden;
    }

    .window-body {
        margin: 2px 0 0 0;
        height: 100%;
        overflow: hidden;
        background-color: rgb(255, 255, 255);
    }

    .sunken-panel {
        overflow-y: auto;
        margin: 2px 0 0 0;
        height: 100%;
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