<script lang="ts">
	type cell = "water" | "ship" | "bomb" | "miss";
	type gridRow = cell[];
	var myGrid: gridRow[] = [
		["water", "water", "water", "water"],
		["water", "water", "water", "water"],
		["water", "water", "water", "water"],
		["water", "water", "water", "water"],
	];

	function displayCell(cell) {
		switch (cell) {
			case "ship":
				return "🚢";
			case "water":
				return "🌊";
			case "bomb":
				return "💥";
			case "miss":
				return "😭";
			default:
				break;
		}
	}

	function displayGrid(grid: gridRow[]) {
		let output = ``;
		grid.forEach((row) => {
			output += `<div class="row">`;
			row.forEach((cell) => {
				output += `<div class="cell"><a onclick={console.log("wefyfewu  ")}>${displayCell(
					cell,
				)}</a></div>`;
			});
			output += `</div>`;
		});
		return (output += ``);
	}
</script>

<div class="grid">
	{@html displayGrid(myGrid)}
</div>
