<script context="module">
    import deckApi from '$lib/api/decks';

    /** @type {import('@sveltejs/kit').Load} */
    export async function load({page}) {
        return {
            // The props are passed to the regular component script
            props: {
                deck: await deckApi.getBySlug(page.params.slug)
            }
        };
    }
</script>

<script>
    import {fade} from 'svelte/transition';
    // access props from the script module and expose them to the markup
    export let deck;
    export let currentCard = deck[0];

    let showFront = true;

    function handleFlip() {
        console.log(deck)
        console.log(currentCard)

        console.log('handling click');
        showFront = !showFront;
    }

    function next() {
        currentCard = deck[(deck.indexOf(currentCard) + 1) % deck.length];
        showFront = true;
    }
</script>

<div class="max-w-3xl mx-auto w-full mt-8">
    <div class="w-full bg-yellow-100 h-96 rounded-md p-4">
        {#if showFront}
            <div transition:fade>
                {currentCard.question}
            </div>
        {:else}
            <div transition:fade>
                {currentCard.answer}
            </div>
        {/if}
    </div>

    <div class="p-6">
        <button class="bg-yellow-400 py-2.5 px-6 rounded-md" on:click={handleFlip}>Flip</button>
        <button class="bg-yellow-400 py-2.5 px-6 rounded-md float-right" on:click={next}>Next</button>
    </div>
</div>

<svelte:head>
    <title>{currentCard.question}</title>
</svelte:head>
