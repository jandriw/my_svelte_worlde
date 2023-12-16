<script lang="ts">
    import Word from "../components/Word.svelte";

    let currentGuess: string[] = []
    let currentGuessIndex: number = 0
    let userGuesses: string[][] = []
    const voidWord: string[] = ["", "", "", "", ""]

    const handleKeydown = (e: KeyboardEvent) => {
        const {key} = e

        if (e.code === "Backspace") {
            currentGuess.pop()
            currentGuess = currentGuess
        } else if (e.key.length === 1 && e.key.match(/[a-z]/i) && currentGuess.length < 5) {
            let letter = e.key.toUpperCase()
            currentGuess = [...currentGuess, letter]
        } else if (e.code === "Enter" && currentGuess.length < 5) {
            //Alert: Not enought letters
        } else if (e.code === "Enter") {
            //Check word and update boardIndex
            userGuesses = [...userGuesses, currentGuess]
            currentGuess = []
            currentGuessIndex += 1
        }
    }

    console.log(currentGuessIndex)
</script>

<svelte:window on:keydown={handleKeydown}/>

<div class="">
    {#each Array(6) as _, i}
        {#if i === currentGuessIndex}
            <Word printedWord={currentGuess} />
        {:else if i < currentGuessIndex}
            <Word printedWord={userGuesses[i]} />
        {:else}
            <Word printedWord={voidWord} />
        {/if}
    {/each}
</div>