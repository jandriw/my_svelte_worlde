<script lang="ts">
    import Letter from '../components/Letter.svelte'

    export let printedWord: string[]
    //export let debugIndex: number

</script>

<div class="flex">
    {#each Array(5) as _, i }
        <Letter {printedWord} letterIndex={i} />
    {/each}

    <!--<p class="text-gray-500 text-2xl">{debugIndex}</p>-->
    
</div>



