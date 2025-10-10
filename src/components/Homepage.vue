<template>
    <div class="homepage">
        <img src="../assets/wordart.png" alt="Word Art" class="img banner">

        <p class="tagline">
            Hi, I'm Jon, a PHP developer specializing in Laravel and Statamic, with other experience ranging 
            from VR development with Unity and C# to WordPress customizations. I solve problems with code and sometimes create new ones.
        </p>

        <div class="chips">
            <span class="chip">PHP</span>
            <span class="chip">Laravel</span>
            <span class="chip">Statamic</span>
            <span class="chip">Unity3D</span>
            <span class="chip">VR</span>
            <span class="chip">Vue.js</span>
        </div>

        <img src="../assets/php.png" alt="PHP" class="img php">

        <p class="footer">
            This site is built with Vue.js and uses the fantastic <a href="https://github.com/jdan/98.css">98.css</a> library.
        </p>
    </div>
</template>

<style scoped>
    .homepage {
        padding: 6px 6px 10px 6px;
        text-align: center;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    p {
        padding: 0 10px 0 10px;
        font-size: 12px;
        line-height: 1.2;
        max-width: 400px;
    }

    .banner {
        margin: 6px 10px 4px 0px;
    }

    .tagline {
        margin: 0px 0 8px 0;
    }

    .chips {
        display: flex;
        flex-wrap: wrap;
        gap: 6px;
        padding: 5px 10px 6px 10px;
        justify-content: center;
    }

    .chip {
        font-size: 11px;
        padding: 2px 6px;
        border: 1px solid #888;
        background-color: #fff;
        box-shadow: inset -1px -1px #000, inset 1px 1px #d1d1d1;
    }

    .actions {
        padding: 0 10px 0 10px;
        align-items: center;
        gap: 6px;
    }

    .actions button {
        min-width: 96px;
    }

    .status {
        padding: 6px 10px 0 10px;
        font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
        font-size: 11px;
        color: #333;
    }

    .img {
        width: 100%;
        max-width: 400px;
        height: auto;
        display: block;
        margin-left: auto;
        margin-right: auto;
    }

    .php {
        width: 100px;
        padding: 10px 0 10px 0;
        animation: rotate 15s linear infinite;
        display: block;
        margin: 0 auto;
    }

    .footer {
        margin-top: 6px;
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