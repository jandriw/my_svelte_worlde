<script lang="ts">
    import Word from "../components/Word.svelte"
    import { correctWords } from "$lib/correctWord";
    import { correctWord } from "$lib/correctWordStore"
	import { onMount } from "svelte";


    type State = 'start' | 'playing' | 'won' | 'lost'

    let state = 'start'
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

    function getRandomInt(max: number) {
        return Math.floor(Math.random() * max);
    }

    function updateCorrectWord() {
        let correctWordId : number = getRandomInt(correctWords.length)
        $correctWord = correctWords[correctWordId]
        console.log($correctWord)
    }

    onMount( 
        () => updateCorrectWord()
    )
</script>

<svelte:window on:keydown={handleKeydown}/>
<div class="flex flex-col">
    <h1 class="text-white text-5xl font-bold my-10 "> Wordle en Español</h1>

    <div class="">
        {#each Array(6) as _, i}
            {#if i === currentGuessIndex}
                <Word printedWord={currentGuess} />
            {:else if i < currentGuessIndex}
                <Word printedWord={userGuesses[i]} validate={true}/>
            {:else}
                <Word printedWord={voidWord} />
            {/if}
        {/each}
    </div>

    <div>
        <!--Resultados-->
    </div>

    <div>
        <!--Teclado-->
    </div>
</div>