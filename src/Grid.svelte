<script lang="ts">
	var size: number = 4;
	var remainingShipsToSpawn: number = Math.ceil(size);
	var remainingShips: number = remainingShipsToSpawn;
	var remainingPlays = size * 2;

	type cell = {
		status: "water" | "ship" | "bomb" | "miss";
		position: { x: number; y: number };
	};
	type gridRow = cell[];
	let grid: gridRow[] = [];

	function populateGrid() {
		while (remainingShipsToSpawn > 0) {
			let x = Math.floor(Math.random() * size);
			let y = Math.floor(Math.random() * size);
			if (grid[x][y].status == "water") {
				grid[x][y].status = "ship";
				remainingShipsToSpawn--;
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
				remainingShips--;
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
	{#if remainingPlays == 0 && remainingShips > 0}
		Você perdeu.
	{:else if remainingShips == 0}
		Você ganhou!
	{:else}
		Tentativas restantes: {remainingPlays}
	{/if}
</div>
