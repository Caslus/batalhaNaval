<script lang="ts">
	import Grid from "./Grid.svelte";

	let unique = {};

	function restart() {
		unique = {};
	}
</script>

<main>
	<h1>Batalha Naval</h1>
	{#key unique}
		<Grid />
	{/key}
	<button on:click={restart}>Reiniciar</button>
</main>
