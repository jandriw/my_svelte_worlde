<script lang="ts">
    import Word from "../components/Word.svelte";

    let currentGuess: string[] = []
    let userGuesses: string[][] = []
    let boardIndex: number = 0

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
            console.log("La palabra debe tener 5 letas")
        } else if (e.code === "Enter") {
            //Check word and update boardIndex
            userGuesses = [...userGuesses, currentGuess]
            currentGuess = []
            boardIndex += 1
            console.log("Cheking word...")
            console.log(userGuesses)
            console.log(boardIndex)
        }
        console.log(currentGuess)
    }

</script>

<svelte:window on:keydown={handleKeydown}/>

{#each Array(6) as _, i}
    <Word {currentGuess} />
{/each}
