<script lang="ts">
	var size: number = 4;
	var remainingShips: number = Math.ceil(size / 2);

	type cell = "water" | "ship" | "bomb" | "miss";
	type gridRow = cell[];
	let grid: gridRow[] = [];

	function populateGrid() {
		for (let i = 0; i < size; i++) {
			let row: cell[] = [];
			for (let j = 0; j < size; j++) {
				if (remainingShips > 0) {
					if (Math.random() > 0.8) {
						grid[i][j] = "ship";
						remainingShips--;
					}
				}
			}
		}
		if (remainingShips > 0) {
			populateGrid();
		}
	}

	function generateGrid() {
		for (let i = 0; i < size; i++) {
			let row: cell[] = [];
			for (let j = 0; j < size; j++) {
				/*if (remainingShips > 0) {
					if (Math.random() > 0.8) {
						row.push("ship");
						remainingShips--;
					} else {
						row.push("water");
					}
				} else {
					row.push("water");
				}*/
				row.push("water");
			}
			grid.push(row);
		}
		populateGrid();
	}
	generateGrid();
</script>

<div class="grid">
	{#each grid as row}
		<div class="row">
			{#each row as cell}
				<div class="cell">
					{#if cell == "water"}
						<!-- svelte-ignore a11y-missing-attribute -->
						<a
							on:click={() => {
								cell = "miss";
							}}
						>
							🌊
						</a>
					{:else if cell == "ship"}
						<!-- svelte-ignore a11y-missing-attribute -->
						<a
							on:click={() => {
								cell = "bomb";
							}}
						>
							🚢
						</a>
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
