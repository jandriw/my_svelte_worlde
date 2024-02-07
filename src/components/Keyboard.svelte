<script lang="ts">
    import { alphabet } from '$lib/Alphabet'
    import { correctLetters, includedLetters, notIncludedLetters } from "$lib/Alphabet"

    $: validateBg = (letter: string) => {
        if ( $correctLetters.includes(letter) ) {
            return "bg-green-500"
        } else if ( $includedLetters.includes(letter) ) {
            return "bg-orange-500"
        } else if ( $notIncludedLetters.includes(letter) ) {
            return "bg-gray-500"
        } else {
            return "bg-transparent"
        }
    }

</script>
<div class="mt-2">
    {#each alphabet as line}
        <div class="flex justify-center">
            {#each line as letter}
                <button class="text-white text-3xl font-bold {validateBg(letter)} border-2 border-white rounded-md m-1 p-1">{letter}</button>
            {/each}
        </div>
    {/each}
</div>