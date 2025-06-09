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
            <div class="sunken-panel">
                <img src="../assets/wordart.png" alt="World Icon" class="wordart">
                <p>
                    This is a simple window component. You can add more content here, such as text, images, or other components.
                    You can also customize the styles to fit your design needs.
                    The title bar contains controls for minimizing, maximizing, and closing the window.
                    The window body can contain any content you like, such as forms, buttons, or lists.
                    You can also add more functionality, such as drag-and-drop or resizing.
                    This is a simple example of a window component in Vue.js.
                    You can use this as a starting point for building more complex applications.
                    Feel free to modify the styles and content to suit your needs.

                    You can also add more components to the window body, such as buttons, forms, or lists.
                    This is a simple example of a window component in Vue.js.
                    You can use this as a starting point for building more complex applications.
                    You can also add more functionality, such as drag-and-drop or resizing.
                    This is a simple example of a window component in Vue.js.
                    You can use this as a starting point for building more complex applications.
                    You can also add more functionality, such as drag-and-drop or resizing.
                    This is a simple example of a window component in Vue.js.
                    You can use this as a starting point for building more complex applications.
                    You can also add more functionality, such as drag-and-drop or resizing.
                    This is a simple example of a window component in Vue.js.
                    You can use this as a starting point for building more complex applications.
                    You can also add more functionality, such as drag-and-drop or resizing.
                </p>
            </div>
        </div>
    </div>
</template>

<style scoped>

    .window {
        width: full;
        height: 300px;
        display: flex;
        flex-direction: column;
    }

    .sunken-panel {
        height: 100%;
        overflow-y: auto;
    }

    .window-body {
        margin: 2px 0 0 0;
        flex: 1;
        min-height: 0;
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