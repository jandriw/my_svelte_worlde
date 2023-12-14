<script lang="ts">
    import Letter from '../components/Letter.svelte'

    export let currentGuess: string[]

    currentGuess = currentGuess

</script>

<div class="flex">
    {#each Array(5) as _, i }
        <Letter {currentGuess} letterIndex={i} />
    {/each}
</div>

<p> {currentGuess} </p>



