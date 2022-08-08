<script lang="ts">
	import backdrop from './assets/backdrop.png';
	import Pattern, { images as i } from './lib/Pattern.svelte';

	let pickedDiagonal = 0;
	let pickedCorner = 1;

	const starfishLeftDiag = [i.STARFISH, i.NONE, i.NONE, i.NONE, i.STARFISH, i.NONE, i.NONE, i.NONE, i.STARFISH];
	const starfishRightDiag = [i.NONE, i.NONE, i.STARFISH, i.NONE, i.STARFISH, i.NONE, i.STARFISH, i.NONE, i.NONE];
	const spiralShellLeftDiag = [i.SPIRAL_SHELL, i.NONE, i.NONE, i.NONE, i.SPIRAL_SHELL, i.NONE, i.NONE, i.NONE, i.SPIRAL_SHELL];
	const spiralShellRightDiag = [i.NONE, i.NONE, i.SPIRAL_SHELL, i.NONE, i.SPIRAL_SHELL, i.NONE, i.SPIRAL_SHELL, i.NONE, i.NONE];
	const diags = [starfishLeftDiag, starfishRightDiag, spiralShellLeftDiag, spiralShellRightDiag];

	const starfishCorner = [i.NONE, i.STARFISH, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE,  i.NONE];
	const spiralShellCorner = [i.NONE, i.SPIRAL_SHELL, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE,  i.NONE];
	const pieceOfAShellCorner = [i.NONE, i.PIECE_OF_A_SHELL, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE,  i.NONE];
	const corners = [starfishCorner, spiralShellCorner, pieceOfAShellCorner];
</script>

<main class="container mx-auto">
	<div class="flex flex-col gap-y-8 items-center p-4">
		<div class="relative max-w-[700px] max-h-[587px]">
			<img src={backdrop} alt="" class=" w-full">
			<div class="backdrop absolute top-0 left-0 grid gap-y-[1px] w-full h-full">
				<div class:invisible="{pickedDiagonal !== 2 || pickedCorner !== 2}" class="marker even:col-start-3 justify-self-end"></div>
				<div class:invisible="{pickedDiagonal !== 3 || pickedCorner !== 0}" class="marker even:col-start-3"></div>
				<div class:invisible="{pickedDiagonal !== 1 || pickedCorner !== 1}" class="marker even:col-start-3"></div>
				<div class:invisible="{pickedDiagonal !== 1 || pickedCorner !== 2}" class="marker even:col-start-3 justify-self-end"></div>
				<div class:invisible="{pickedDiagonal !== 2 || pickedCorner !== 0}" class="marker even:col-start-3 row-start-4"></div>
				<div class:invisible="{pickedDiagonal !== 0 || pickedCorner !== 2}" class="marker even:col-start-3 row-start-4 justify-self-end"></div>
				<div class:invisible="{pickedDiagonal !== 0 || pickedCorner !== 1}" class="marker even:col-start-3 row-start-6 justify-self-end"></div>
				<div class:invisible="{pickedDiagonal !== 3 || pickedCorner !== 2}" class="marker even:col-start-3 row-start-6"></div>
			</div>
		</div>

		<div class="flex flex-row gap-x-8 justify-center w-full">
			{#each diags as diag, i}
				<label class="flex flex-col gap-2 p-2 bg-zinc-800 rounded border-2 border-zinc-900 cursor-pointer" class:bg-slate-800={pickedDiagonal === i} class:border-slate-900={pickedDiagonal === i}>
					<input type="radio" name="pickedDiagonal" bind:group={pickedDiagonal} value={i}>
					<Pattern items={diag}/>
				</label>
			{/each}
		</div>

		<div class="flex flex-row gap-x-8 justify-center w-full">
			{#each corners as corner, i}
				<label class="flex flex-col gap-2 p-2 bg-zinc-800 rounded border-2 border-zinc-900 cursor-pointer" class:bg-slate-800={pickedCorner === i} class:border-slate-900={pickedCorner === i} class:hidden={Math.floor(pickedDiagonal/2) === i}>
					<input type="radio" name="pickedCorner" bind:group={pickedCorner} value={i}>
					<Pattern items={corner}/>
				</label>
			{/each}
		</div>
	</div>

</main>

<style>
	.backdrop {
		grid-template:
			"a . b" 1fr
			"c . d" 1fr
			". . ." 0.8fr
			"e . f" 1fr
			". . ." 0.3fr
			"g . h" 1fr / 2.75fr 1fr 2.75fr;
	}
	.marker {
		@apply w-[38%] h-full bg-green-500 opacity-50;
	}

</style>