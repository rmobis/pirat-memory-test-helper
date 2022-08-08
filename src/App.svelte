<script lang="ts">
	import backdrop from './assets/backdrop.png';
	import Pattern, { images as i } from './lib/Pattern.svelte';

	let pickedDiagonal = 0;
	let pickedCorner = 1;;

	$: console.log(pickedDiagonal);

	const starfishLeftDiag = [i.STARFISH, i.NONE, i.NONE, i.NONE, i.STARFISH, i.NONE, i.NONE, i.NONE, i.STARFISH];
	const starfishRightDiag = [i.NONE, i.NONE, i.STARFISH, i.NONE, i.STARFISH, i.NONE, i.STARFISH, i.NONE, i.NONE];
	const spiralShellLeftDiag = [i.SPIRAL_SHELL, i.NONE, i.NONE, i.NONE, i.SPIRAL_SHELL, i.NONE, i.NONE, i.NONE, i.SPIRAL_SHELL];
	const spiralShellRightDiag = [i.NONE, i.NONE, i.SPIRAL_SHELL, i.NONE, i.SPIRAL_SHELL, i.NONE, i.SPIRAL_SHELL, i.NONE, i.NONE];
	const diags = [starfishLeftDiag, starfishRightDiag, spiralShellLeftDiag, spiralShellRightDiag];

	const starfishCorner = [i.NONE, i.STARFISH, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE,  i.NONE];
	const spiralShellCorner = [i.NONE, i.SPIRAL_SHELL, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE,  i.NONE];
	const pieceOfAShellCorner = [i.NONE, i.PIECE_OF_A_SHELL, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE, i.NONE,  i.NONE];
</script>

<main class="container mx-auto">
	<div class="flex flex-col gap-y-8 items-center p-4">
		<div class="bg-cover grid grid-cols-2 gap-x-28 w-[700px] h-[587px]" style:background-image="url({backdrop})">
			<div class:invisible="{pickedDiagonal !== 2 || pickedCorner !== 2}" class="w-28 h-28 bg-green-500 opacity-50 justify-self-end"></div>
			<div class:invisible="{pickedDiagonal !== 3 || pickedCorner !== 0}" class="w-28 h-28 bg-green-500 opacity-50"></div>
			<div class:invisible="{pickedDiagonal !== 1 || pickedCorner !== 1}" class="w-28 h-28 bg-green-500 opacity-50"></div>
			<div class:invisible="{pickedDiagonal !== 1 || pickedCorner !== 2}" class="w-28 h-28 bg-green-500 opacity-50 justify-self-end"></div>
			<div class="h-24 col-span-2 opacity-0"></div>
			<div class:invisible="{pickedDiagonal !== 2 || pickedCorner !== 0}" class="w-28 h-28 bg-green-500 opacity-50"></div>
			<div class:invisible="{pickedDiagonal !== 0 || pickedCorner !== 2}" class="w-28 h-28 bg-green-500 opacity-50 justify-self-end"></div>
			<div class="h-6 col-span-2 opacity-0"></div>
			<div class:invisible="{pickedDiagonal !== 0 || pickedCorner !== 1}" class="w-28 h-28 bg-green-500 opacity-50 justify-self-end"></div>
			<div class:invisible="{pickedDiagonal !== 3 || pickedCorner !== 2}" class="w-28 h-28 bg-green-500 opacity-50"></div>
		</div>

		<div class="flex flex-row gap-x-8 justify-center w-full">
			{#each diags as diag, i}
				<label class="flex flex-col gap-2 p-2 bg-gray-200 rounded border-2 border-gray-400 cursor-pointer" class:bg-gray-400={pickedDiagonal === i} class:border-gray-700={pickedDiagonal === i}>
					<input type="radio" name="pickedDiagonal" bind:group={pickedDiagonal} value={i}>
					<Pattern items={diag}/>
				</label>
			{/each}
		</div>

		<div class="flex flex-row gap-x-8 justify-center w-full">
			{#each corners as corner, i}
				<label class="flex flex-col gap-2 p-2 bg-gray-200 rounded border-2 border-gray-400 cursor-pointer" class:bg-gray-400={pickedCorner === i} class:border-gray-700={pickedCorner === i} class:hidden={Math.floor(pickedDiagonal/2) === i}>
					<input type="radio" name="pickedCorner" bind:group={pickedCorner} value={i}>
					<Pattern items={corner}/>
				</label>
			{/each}
		</div>
	</div>

</main>

<style>
</style>