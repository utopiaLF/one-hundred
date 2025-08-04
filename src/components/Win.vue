<template>
    <div class="wonDiv" :class="{ active: won}">
        <img src="https://i.gifer.com/Xtef.gif" width="90" alt="">
        <h1>Correct! You guessed in {{ guessCount }} tries</h1>
        <button @click="$emit('refreshPage')" class="playAgainBtn">Play Again</button>
    </div>
</template>

<script>
export default {
    props: ['guessCount', 'won'],
    emits: ['refreshPage']
}
</script>