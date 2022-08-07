<script lang="ts">

	import none from '../assets/none.png';
	import starfish from '../assets/starfish.gif';
	import spiralShell from '../assets/spiral-shell.gif';
	import pieceOfAShell from '../assets/piece-of-a-shell.gif';

	export const images = Object.freeze({
		NONE: none,
		STARFISH: starfish,
		SPIRAL_SHELL: spiralShell,
		PIECE_OF_A_SHELL: pieceOfAShell
	});

	export let items = Array(9).fill(images.NONE);
</script>

<div class="grid grid-cols-3 place-content-center">
	{#each items as item}
		<img class="w-8 h-8" src={item} alt="">
	{/each}
</div>
