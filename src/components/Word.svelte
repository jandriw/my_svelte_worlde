<script lang="ts">
    import Letter from '../components/Letter.svelte'

    export let printedWord: string[]
    export let validate: boolean = false

</script>



<div class="flex mb-2">
    {#each Array(5) as _, i }
        <Letter {printedWord} letterIndex={i} {validate} />
    {/each}

    <!--<p class="text-gray-500 text-2xl">{validate}</p>-->
    
</div>



