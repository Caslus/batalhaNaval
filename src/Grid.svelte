<script lang="ts">
	type cell = "water" | "ship" | "bomb" | "miss";
	type gridRow = cell[];
	var myGrid: gridRow[] = [
		["water", "water", "water", "water"],
		["water", "water", "water", "water"],
		["water", "water", "water", "water"],
		["water", "water", "water", "water"],
	];
</script>

<div class="grid">
	{#each myGrid as row}
		<div class="row">
			{#each row as cell}
				<div class="cell">
					{#if cell == "water"}
						🌊
					{:else if cell == "ship"}
						🚢
					{:else if cell == "bomb"}
						💥
					{:else if cell == "miss"}
						😭
					{/if}
				</div>
			{/each}
		</div>
	{/each}
</div>
