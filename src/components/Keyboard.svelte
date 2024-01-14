<script>
    import { alphabet } from '$lib/Alphabet'
</script>
<div class="mt-2">
    {#each alphabet as line}
        <div class="flex justify-center">
            {#each line as letter}
                <button class="text-white text-3xl border-2 border-white rounded-md m-1 p-1">{letter}</button>
            {/each}
        </div>
    {/each}
</div>