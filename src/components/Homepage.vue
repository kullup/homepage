<template>
    <img src="../assets/wordart.png" alt="Word Art" class="img">
    <p>
        The quick brown fox jumps over the lazy dog. This is a classic pangram used to test fonts and keyboards.
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et
        dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex
        ea commodo consequat.
    </p>
    <img src="../assets/php.png" alt="Word Art" class="img php">
    <p>
        PHP is a popular general-purpose scripting language that is especially suited to web development. Fast,
        flexible and pragmatic, PHP powers everything from your blog to the most popular websites in the world.
    </p>
    <p>
        This is a simple text paragraph to demonstrate the layout of the window. It contains multiple lines of text
        to show how the content flows within the window.
        You can add more text here to see how it behaves with different lengths and styles.
    </p>
    <p>
        Another paragraph to further illustrate the text wrapping and layout capabilities of this window component.
        Feel free to modify the content as needed.
    </p>
    <p>
        This is the last paragraph in this example. It serves to show how the text appears at the bottom of the
        window, ensuring that everything fits nicely within the defined space.
    </p>
</template>

<style scoped>
    p {
        padding: 0 10px 0 10px;
        font-size: 12px;
        line-height: 1.2;
    }

    .img {
        width: 100%;
        max-width: 400px;
        height: auto;
    }

    .php {
        width: 100px;
        padding: 10px 0 10px 0;
        animation: rotate 15s linear infinite;
    }

    @keyframes rotate {
        from {
            transform: rotate(0deg);
        }
        to {
            transform: rotate(360deg);
        }
    }
</style>