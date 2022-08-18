<script lang="ts">
	var size: number = 4;
	var remainingShips: number = Math.ceil(size);
	var remainingPlays = size * 2;

	type cell = {
		status: "water" | "ship" | "bomb" | "miss";
		position: { x: number; y: number };
	};
	type gridRow = cell[];
	let grid: gridRow[] = [];

	function populateGrid() {
		while (remainingShips > 0) {
			let x = Math.floor(Math.random() * size);
			let y = Math.floor(Math.random() * size);
			if (grid[x][y].status == "water") {
				grid[x][y].status = "ship";
				remainingShips--;
			}
		}
	}

	function generateGrid() {
		for (let i = 0; i < size; i++) {
			let row: cell[] = [];
			for (let j = 0; j < size; j++) {
				row.push({ status: "water", position: { x: i, y: j } });
			}
			grid.push(row);
		}
		populateGrid();
	}
	generateGrid();

	function play(cell: cell) {
		if (remainingPlays > 0) {
			if (cell.status == "water") {
				grid[cell.position.x][cell.position.y].status = "miss";
			} else {
				grid[cell.position.x][cell.position.y].status = "bomb";
			}
			remainingPlays--;
		}
	}
</script>

<div class="grid">
	{#each grid as row}
		<div class="row">
			{#each row as cell}
				<div class="cell">
					{#if cell.status == "water"}
						<!-- svelte-ignore a11y-missing-attribute -->
						<a
							on:click={() => {
								play(cell);
							}}
						>
							🌊
						</a>
					{:else if cell.status == "ship"}
						<!-- svelte-ignore a11y-missing-attribute -->
						<a
							on:click={() => {
								play(cell);
							}}
						>
							🚢
						</a>
					{:else if cell.status == "bomb"}
						💥
					{:else if cell.status == "miss"}
						😭
					{/if}
				</div>
			{/each}
		</div>
	{/each}
</div>
<div>
	Tentativas restantes: {remainingPlays}
</div>
