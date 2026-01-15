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
            <div class="divider-container">
                <div class="divider"></div>
            </div>
            <p class="ibm-plex-mono-medium">
                I’m Jon, I develop Software based on <span>PHP</span> and <span>Laravel</span>.
            </p>
        </div>
    </div>
</template>
<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');
    span {
        color: #41a728;
    }
    pre {
        background-color: transparent;
        box-shadow: none;
        padding: none;
    }

    p {
        text-align: left;
        padding: 0 10px 0 10px;
        max-width: 400px;
    }

    span {
        text-decoration: underline;
    }


    .divider {
        width: 100%;
        height: 1px;
        border-bottom: 1px solid #41a728;
        border-style: dotted;
        margin: 0px 10px 0px 10px;
    }

    .divider-container {
        width: 100%;
        max-width: 400px;
        display: flex;
        justify-content: center;
        align-items: center;
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
            font-size: 0.5rem;
        }
    }

    @media (max-width: 450px) {
        .heading {
            font-size: 0.25rem;
        }
    }
</style>