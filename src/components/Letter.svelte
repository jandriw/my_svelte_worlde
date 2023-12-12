<script>
    export let word
    export let letterIndex

    $: letter = word[letterIndex] || ""

    //if (word[letterIndex] !== undefined) {
    //    letter = word[letterIndex]
    //}

    console.log("word desde Letter:", word)
    console.log("letterIndex:", letterIndex)
    console.log("letter:", letter)

</script>



<div class="h-16 w-16 border-[3px] rounded-md border-yellow-50 text-white font-bold text-5xl flex items-center justify-center leading-none">
    {letter}
</div>