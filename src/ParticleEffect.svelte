<!-- ParticleEffect.svelte -->

<script>
    import { onMount, onDestroy } from "svelte";

    let flakes = [];

    onMount(() => {
        var getV = function () {
            return 5 * (Math.random() - 0.5);
        };

        function Flake() {
            this._node = document.createElement("div");
            this._node.className = "flake";

            this._vec = { x: getV(), y: getV() };
            this._pos = { x: this._vec.x * 40, y: this._vec.y * 40 - 10 };

            this._scale = 2 + Math.random();
            this._scale = Math.max(0, this._scale - 0.03 * 60);

            if (this._pos.x * this._pos.x + this._pos.y * this._pos.y < 8000) {
                this._render();
            }
        }

        Flake.prototype = {
            getNode: function () {
                return this._node;
            },

            update: function () {
                if (!this._pos) {
                    this._pos = { x: 0, y: 0 };
                    this._vec = { x: getV(), y: getV() };
                    this._scale = 2 + Math.random();
                }

                this._vec.y += 0.05;

                this._pos.x += this._vec.x;
                this._pos.y += this._vec.y;
                this._scale = Math.max(0, this._scale - 0.035);

                this._render();

                if (
                    this._pos.x * this._pos.x + this._pos.y * this._pos.y >
                    100000
                ) {
                    this._pos = null;
                }
            },

            _render: function () {
                var transform =
                    "translate3d(" +
                    this._pos.x +
                    "px," +
                    this._pos.y +
                    "px,0) scale(" +
                    this._scale +
                    ")";

                this._node.style["msTransform"] = transform;
                this._node.style["webkitTransform"] = transform;
                this._node.style["MozTransform"] = transform;
                this._node.style["OTransform"] = transform;
                this._node.style["transform"] = transform;
                this._node.style.background = "#FFFFFF";
                this._node.style.zIndex = 100000;

            },
        };

        const MAX_FLAKES = 300;
        const orb = document.querySelector(".orb");
        flakes = new Array(MAX_FLAKES);
        let flake;

        // setup flakes
        for (let i = 0; i < MAX_FLAKES; i++) {
            flake = new Flake();
            const node = flake.getNode();
            orb.appendChild(node);
            flakes[i] = flake;
        }

        // the flake creator
        const tick = function () {
            // update flakes
            for (let i = 0; i < MAX_FLAKES; i++) {
                flake = flakes[i];
                flake.update();
            }

            // next tick
            requestAnimationFrame(function () {
                tick();
            });
        };

        // start ticking
        setTimeout(() => {
            tick();
        }, 250);

        // Cleanup on component destruction
        // onDestroy(() => {
        //     flakes.forEach((flake) => {
        //         const node = flake.getNode();
        //         orb.removeChild(node);
        //     });
        // });
    });
</script>

<div class="orb"></div>

<style>
    @keyframes glow {
        from {
            transform: scale(1);
        }

        to {
            transform: scale(1.125);
        }
    }

    .orb {
        display: inline-block;
        position: relative;
        top: 50%;
        transform: translateY(-50%);
        width: 2rem;
        height: 2rem;
        background: #fff;
        box-shadow:
            0 0 80px #ebd4ff,
            0 0 20px #f6ffe1,
            0 0 10px #f6ffe1;
        border-radius: 50%;
        filter: blur(1px);

        &::after,
        &::before {
            position: absolute;
            animation-name: glow;
            animation-iteration-count: infinite;
            animation-direction: alternate;
            top: 50%;
            left: 50%;
            content: "";
            background: radial-gradient(
                ellipse at center,
                rgba(240, 255, 255, 0.05) 0%,
                rgba(240, 255, 255, 0) 50%
            );
        }

        &::after {
            animation-duration: 1s;
            width: 40rem;
            height: 0.5rem;
            margin-left: -20rem;
            margin-top: -0.25rem;
        }

        &::before {
            animation-duration: 0.25s;
            width: 20rem;
            height: 2rem;
            margin-left: -10rem;
            margin-top: -1rem;
        }
    }

    .flake {
        position: absolute;
        left: 50%;
        top: 50%;
        background: #fff;
        width: 0.25rem;
        height: 0.25rem;
        margin-top: -0.125rem;
        margin-left: -0.125rem;
        border-radius: 50%;
        box-shadow:
            0 0 20px #f6ffe1,
            0 0 10px #f6ffe1;
    }
</style>
