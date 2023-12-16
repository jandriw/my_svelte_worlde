<script lang="ts">
    export let printedWord: string []
    export let letterIndex: number

    let voidSpot: string = ""

</script>

<div class="h-16 w-16 border-[3px] rounded-md border-yellow-50 text-white font-black text-5xl flex items-center justify-center leading-none">
    {#if printedWord[letterIndex] === undefined}
        {voidSpot}
    {:else}
        {printedWord[letterIndex]}
    {/if}
</div>