<script>
	import DeckCard from '$lib/DeckCard.svelte';
	export let decks;
</script>

<ul class="space-y-4">
	{#each decks as deck (deck.slug)}
		<DeckCard {deck} />
	{/each}
</ul>
