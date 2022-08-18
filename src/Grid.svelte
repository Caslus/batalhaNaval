<script lang="ts">
	var size: number = 4;
	var remainingShips: number = Math.ceil(size);
	var remainingPlays = size * 2;

	type cell = "water" | "ship" | "bomb" | "miss";
	type gridRow = cell[];
	let grid: gridRow[] = [];

	function populateGrid() {
		while (remainingShips > 0) {
			let x = Math.floor(Math.random() * size);
			let y = Math.floor(Math.random() * size);
			if (grid[x][y] == "water") {
				grid[x][y] = "ship";
				remainingShips--;
			}
		}
	}

	function generateGrid() {
		for (let i = 0; i < size; i++) {
			let row: cell[] = [];
			for (let j = 0; j < size; j++) {
				row.push("water");
			}
			grid.push(row);
		}
		populateGrid();
	}
	generateGrid();

	function play(cell: cell) {
		if (remainingPlays > 0) {
			if (cell == "water") {
				cell = "miss";
			} else {
				cell = "bomb";
			}
			remainingPlays--;
			console.log(remainingPlays);
		}
	}
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
								play(cell);
							}}
						>
							🌊
						</a>
					{:else if cell == "ship"}
						<!-- svelte-ignore a11y-missing-attribute -->
						<a
							on:click={() => {
								play(cell);
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
