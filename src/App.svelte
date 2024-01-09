<script>
	import { onMount } from "svelte";
	export let name;
	import HexagonalProgressBar from "./HexagonalProgressBar.svelte";
	import ParticleEffect from "./ParticleEffect.svelte";

	onMount(() => {
		console.log(heroElement);
		loaded = true;
	});

	let heroElement;
	let loaded = false;
</script>

<main id="effect" bind:this={heroElement}>
	<HexagonalProgressBar />
</main>
{#if loaded}
	<ParticleEffect bind:el={heroElement} />
{/if}

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
