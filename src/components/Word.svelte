<script>
    import Letter from '../components/Letter.svelte'

    export let currentGuess

    $: word = currentGuess

    console.log("word desde Word:", word)
</script>

<div class="flex">
    {#each Array(5) as _, i }
        <Letter {word} letterIndex={i} />
    {/each}
</div>



