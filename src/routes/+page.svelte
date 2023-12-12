<script>
    import Word from "../components/Word.svelte";

    let currentGuess = []

    const handleKeydown = (e) => {
        let word = e.key.toUpperCase()
        currentGuess.push(word)
        console.log("currentGuess desde page:", currentGuess)
    }

</script>

<svelte:window on:keydown={handleKeydown}/>

<Word {currentGuess}/>
