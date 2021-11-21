<script context="module">
	import deckApi from '$lib/api/decks';

	/** @type {import('@sveltejs/kit').Load} */
	export async function load({ page }) {
		return {
			// The props are passed to the regular component script
			props: {
				deck: await deckApi.getBySlug(page.params.slug)
			}
		};
	}
</script>

<script>
	import { fade } from 'svelte/transition';
	// access props from the script module and expose them to the markup
	export let deck;

	let showFront = true;

	function handleFlip() {
		console.log('handling click');
		showFront = !showFront;
	}
</script>

<div class="max-w-3xl mx-auto w-full mt-8">
	<div class="flex justify-center items-center h-full mt-16">
		<div class="w-full bg-yellow-100 h-96 rounded-md">
			{#if showFront}
				<div transition:fade>
					{deck[0].question}
				</div>
			{:else}
				<div transition:fade>
					{deck[0].answer}
				</div>
			{/if}
		</div>

		<button class="bg-yellow-400 py-2.5 px-6 rounded-md" on:click={handleFlip}>Flip</button>
	</div>
</div>

<svelte:head>
	<title>{deck}</title>
</svelte:head>
