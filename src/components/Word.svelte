<script lang="ts">
    import Letter from '../components/Letter.svelte'
    import { fade } from 'svelte/transition'

    export let printedWord: string[]
    export let validate: boolean = false

    let i: number = 0 

    $: transition = validate ? { delay: 2000 * i } : { delay: 0 }

</script>

<div class="flex mb-2">
    {#each Array(5) as _, i }
        <div in:fade={transition}>
            <Letter {printedWord} letterIndex={i} {validate} />
        </div>
    {/each}

    <!--<p class="text-gray-500 text-2xl">{validate}</p>-->
    
</div>



