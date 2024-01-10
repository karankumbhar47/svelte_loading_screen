<script>
    import { onMount, onDestroy } from "svelte";
	import ParticleEffect from "./ParticleEffect.svelte";
    export let xCor;

    let max = 2160;

    const updateProgress = (value, percent) => {
        value
            .querySelector(".fill")
            .setAttribute(
                "style",
                `stroke-dashoffset: ${((100 - percent) / 100) * max}`,
            );
        value.querySelector(".value").innerHTML = `${percent}%`;
        const rect = value.getBoundingClientRect();
        const top = rect.top + window.scrollY;
    };

    onMount(() => {
        const value = document.querySelector(".progress");
        updateProgress(value, 0);

        const rect = value.getBoundingClientRect();

        const interval = setInterval(() => {
            updateProgress(
                value,
                parseInt(value.querySelector(".value").innerHTML, 10) + 1,
            );
            if (parseInt(value.querySelector(".value").innerHTML, 10) === 100) {
                clearInterval(interval);
            }
        }, 50);
    });
</script>

<div id="wrapper" class="center">
    <svg
        class="progress blue noselect"
        data-progress=""
        x="0px"
        y="0px"
        viewBox="0 0 776 628"
    >
        <path
            class="fill"
            d="M723 314L543 625.77 183 625.77 3 314 183 2.23 543 2.23 723 314z"
        ></path>
        <text class="value" x="50%" y="61%">0%</text>
    </svg>
</div>
<div class="particle-container">
    <ParticleEffect bind:xCor />
</div>

<style>
    @import url("https://fonts.googleapis.com/css?family=Open+Sans:400,700");

    body {
        background: rgb(35, 51, 64);
    }

    #wrapper {
        position: relative;
        top: 80px;
        width: 404px;
    }

    .center {
        left: 50%;
        -webkit-transform: translate(-50%);
        -ms-transform: translate(-50%);
        transform: translate(-50%);
    }

    .progress {
        width: 200px;
        height: 240px;
    }

    .progress .track,
    .progress .fill {
        fill: rgba(0, 0, 0, 0);
        stroke-width: 10;
        transform: translate(290px, 800px) rotate(-120deg);
    }

    .progress .track {
        stroke: rgb(56, 71, 83);
    }

    .progress .fill {
        stroke: rgb(255, 255, 255);
        stroke-linecap: round;
        stroke-dasharray: 2160;
        stroke-dashoffset: 2160;
        transition: stroke-dashoffset 1s;
    }

    .progress.blue .fill {
        stroke: #f3c156;
    }

    .progress .value,
    .progress .text {
        font-family: "Open Sans";
        fill: rgb(255, 255, 255);
        text-anchor: middle;
    }

    .progress .value {
        font-size: 180px;
    }

    .progress .text {
        font-size: 120px;
    }

    .noselect {
        -webkit-touch-callout: none;
        -webkit-user-select: none;
        -khtml-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        cursor: default;
    }
</style>
