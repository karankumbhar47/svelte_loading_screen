<script>
     import { onMount, onDestroy } from 'svelte';

let max = 2160;

const updateProgress = (value, percent) => {
  value.querySelector('.fill').setAttribute('style', `stroke-dashoffset: ${((100 - percent) / 100) * max}`);
  value.querySelector('.value').innerHTML = `${percent}%`;
};

onMount(() => {
  document.querySelectorAll('.progress').forEach((value) => {
    const percent = value.getAttribute('data-progress');

    // Initial update
    updateProgress(value, 0);

    // Update progress over time (simulating loading)
    const interval = setInterval(() => {
      updateProgress(value, parseInt(value.querySelector('.value').innerHTML, 10) + 1);

      // Stop the interval when reaching 100%
      if (parseInt(value.querySelector('.value').innerHTML, 10) === 100) {
        clearInterval(interval);
      }
    }, 50);
  });
});

onDestroy(() => {
  // Cleanup code if needed
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
        <!-- <path
            class="track"
            d="M723 314L543 625.77 183 625.77 3 314 183 2.23 543 2.23 723 314z"
        ></path> -->
        <path
            class="fill"
            d="M723 314L543 625.77 183 625.77 3 314 183 2.23 543 2.23 723 314z"
        ></path>
        <text class="value" x="50%" y="61%">0%</text>
        <!-- <text class="text" x="50%" y="122%">Loading ...</text> -->
    </svg>
    <!-- <svg
        class="progress green noselect"
        data-progress="100"
        x="0px"
        y="0px"
        viewBox="0 0 776 628"
    >
        <path
            class="track"
            d="M723 314L543 625.77 183 625.77 3 314 183 2.23 543 2.23 723 314z"
        ></path>
        <path
            class="fill"
            d="M723 314L543 625.77 183 625.77 3 314 183 2.23 543 2.23 723 314z"
        ></path>
        <text class="value" x="50%" y="61%">0%</text>
        <text class="text" x="50%" y="122%">Green</text>
    </svg> -->
</div>

<style>
    /*===== Not The CSS :P =====*/
    @import url("https://fonts.googleapis.com/css?family=Open+Sans:400,700");
    body {
        background: rgb(35, 51, 64);
    }
    /* h1 {
        font-family: "Open Sans";
        color: rgb(255, 255, 255);
        text-align: center;
        margin: 50px 0 -80px;
    }
    a {
        font-family: "Open Sans";
        color: rgb(255, 255, 255);
        margin: 50px 0 -80px;
        text-align: center;
        width: 100%;
        font-size: 12px;
        text-decoration: none;
    } */
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

    /*===== The CSS =====*/
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
    /* .progress.green .fill {
        stroke: rgb(186, 223, 172);
    } */ 
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
