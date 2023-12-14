<script lang="ts">
    export let currentGuess: string []
    export let letterIndex: number

    let voidSpot: string = ""

</script>

<div class="h-16 w-16 border-[3px] rounded-md border-yellow-50 text-white font-bold text-5xl flex items-center justify-center leading-none">
    {#if currentGuess[letterIndex] === undefined}
        {voidSpot}
    {:else}
        {currentGuess[letterIndex]}
    {/if}
</div>