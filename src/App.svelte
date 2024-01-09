<script>
	import { onMount } from "svelte";
	export let name;
	import HexagonalProgressBar from "./HexagonalProgressBar.svelte";
	import ParticleEffect from "./ParticleEffect.svelte";
</script>

<main>
	<HexagonalProgressBar />
	<ParticleEffect />
</main>

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
  
