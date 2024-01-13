<script lang="ts">
    import Word from "../components/Word.svelte"
    import { correctWords } from "$lib/correctWord"
    import { correctWord } from "$lib/correctWordStore"
	import { onMount } from "svelte"


    type State = 'start' | 'playing' | 'won' | 'lost'

    let state: State = 'start'
    let currentGuess: string[] = []
    let currentGuessIndex: number = 0
    let userGuesses: string[][] = []
    let lastWord: string = ''
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
            lastWord = currentGuess.join("").toUpperCase()
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

    function gameWon() {
        state = 'won'
        console.log(state)
    }

    function gameLost() {
        state = 'lost'
        console.log(state)
    }

    $: lastWord === $correctWord.toUpperCase() && gameWon()
    $: currentGuessIndex >= 6 && lastWord !== $correctWord.toUpperCase() && gameLost()



</script>

<svelte:window on:keydown={handleKeydown}/>

{#if state === 'start'}

        <h1 class="flex justify-center text-white font-bold text-6xl mt-36 mb-10">Wordle en Español</h1>
        <button class="flex m-auto text-white font-bold text-3xl bg-blue-500 rounded-md hover:bg-blue-400 px-5 py-1" on:click={() => state = 'playing'}>Empezar 🎉</button>


{:else}

<div class="flex flex-col">
    <h1 class="text-white text-5xl font-bold my-10 m-auto"> Wordle en Español</h1>

    <div class="m-auto">
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

    <div class="m-auto">
        <!--Resultados-->
        {#if state === 'won'}
            <h1 class="text-white text-3xl font-bold my-10 m-auto"> 🎉 !!Has Ganado!! 🎉 </h1>
        {:else if state === 'lost'}
            <h1 class="text-white text-3xl font-bold my-10 m-auto"> 💩 Has Perdido... 💩 </h1>
            <h1 class="text-white text-3xl font-bold my-10 m-auto"> La palabra secreta era "{$correctWord}" </h1>
        {/if}
    </div>

    <div class="m-auto">
        <!--Teclado-->
    </div>
</div>

{/if}
