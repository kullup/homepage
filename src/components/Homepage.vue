<template>
    <div class="homepage">
        <div class="terminal">
            <pre class="ibm-plex-mono-medium heading">
██╗  ██╗███████╗██╗     ██╗      ██████╗ ██╗
██║  ██║██╔════╝██║     ██║     ██╔═══██╗██║
███████║█████╗  ██║     ██║     ██║   ██║██║
██╔══██║██╔══╝  ██║     ██║     ██║   ██║╚═╝
██║  ██║███████╗███████╗███████╗╚██████╔╝██╗
╚═╝  ╚═╝╚══════╝╚══════╝╚══════╝ ╚═════╝ ╚═╝</pre>
            <p class="ibm-plex-mono-medium">
                I'm Jon. I work as a php/Laravel developer.
            </p>
        </div>
    </div>
</template>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');

    pre {
        background-color: transparent;
        box-shadow: none;
        padding: none;
    }

    p {
        text-align: center;
    }

    .terminal {
        margin: auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .ibm-plex-mono-medium {
        font-family: "IBM Plex Mono", monospace;
        font-weight: 500;
        font-style: normal;
        color: #41a728;
    }

    .homepage {
        display: flex;
        flex-direction: column;
        align-items: start;
        justify-content: start;
        width: 100%;
        height: 100%;
        background-color: #000000
    }    

    @media (max-width: 768px) {
        .heading {
            font-size: 0.4rem;
        }
    }
</style>