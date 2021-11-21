<script>
	import DeckCardList from '$lib/DeckCardList.svelte';
	import deckApi from '$lib/api/decks';

	export const deckPromise = deckApi.getDecks();
</script>

<svelte:head>
	<title>Decks</title>
</svelte:head>

<main class="max-w-3xl mx-auto w-full mt-8">
	<h1>Pick a deck to get started</h1>

	{#await deckPromise}
		<!-- promise is pending -->
		<p>waiting for the promise to resolve...</p>
	{:then data}
		<DeckCardList decks={data} />
	{:catch error}
		<!-- promise was rejected -->
		<p>Something went wrong: {error.message}</p>
	{/await}
</main>
