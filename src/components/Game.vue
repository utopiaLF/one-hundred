<template>
     <h2>Guess the number between 1 and 100</h2>
    <input ref="guessInput" :value="number" @input="$emit('update:number', $event.target.value)" @keyup.enter="$emit('guessTheNumber')" type="number" placeholder="Your number...">
    <button @click="$emit('guessTheNumber')" class="guessBtn" :class="{ active: number}" :disabled="!number">Guess</button>
    <br>
    <transition name="fade">
        <p v-if="alertMessage">{{ alertMessage }}</p>
    </transition>
</template>

<script>
export default {
    props: ['number', 'alertMessage'],
    emits: ['guessTheNumber', 'update:number'],
    methods: {
        blurInput() {
            this.$refs.guessInput.blur()
        }
    }
}
</script>