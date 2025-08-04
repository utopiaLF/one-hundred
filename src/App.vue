<template>
    <Game ref="child" v-model:number="number" :alert-message="alertMessage" @guess-the-number="guessTheNumber"/>
    <Win :guess-count="guessCount" :won="won" @refresh-page="refreshPage"/>
</template>

<script>
import Game from './components/Game.vue';
import Win from './components/Win.vue';

export default {
    components: {
        Game,
        Win
    },
    data() {
        return {
            number: null,
            guessCount: 0,
            alertMessage: '',
            won: false
        }
    },
    methods: {
        guessTheNumber() {
            this.guessCount++;
            const randomNumberIs = sessionStorage.getItem('randomNumberIs') || 0;

            if (this.number < randomNumberIs) {
                this.alertMessage = 'Too low. Try a higher number.'
            } else if (this.number > randomNumberIs) {
                this.alertMessage = 'Too high. Try a lower number.'
            } else if (this.number == randomNumberIs) {
                this.alertMessage = 'Congratulations! You guessed it!';
                this.won = true;
                
                confetti({
                    particleCount: 150,
                    spread: 70,
                    origin: { y: 0.6 }
                });
                this.$refs.child.blurInput();
            } else {
                this.alertMessage = 'Pls enter a number between 1 and 100.'
            }
        },
        refreshPage() {
            window.location.reload();
        }
    },
    mounted() {
        const randomNumber = Math.floor(Math.random() * 100) + 1;
        sessionStorage.setItem('randomNumberIs', randomNumber);
    }
}
</script>