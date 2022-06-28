<template>    
    <div class="indecision-container">
        <h1>Hacele una pregunta al akinator</h1>
        <span>¡Recordá hacer tu pregunta con signo de interrogación al final: (?)</span>
        <br>
        <input type="text" v-model="question" placeholder="Tu pregunta es...">
    </div>
    <div class="answer-container">
        <img v-bind="akinatorStatus" :src="images[akinatorStatus]" alt="Akinator">
        <div v-if="isValidQuestion">
            <p class="speech-text">{{answer}}</p>
            <img class="back" v-if="gif" :src="gif" alt="bg">
        </div>
    </div>
</template>
<script>
export default {
    name: 'Indecision',
    data() {
        return {
            question: null,
            answer: null,
            gif: null,
            isValidQuestion: false,
            akinatorStatus: 0,
            images: [
                'https://www.blogodisea.com/wp-content/uploads/2009/05/akinator.png',
                'https://4.bp.blogspot.com/_o40I1NXKJF8/SwKggPivX_I/AAAAAAAAEVU/sesarvVjhLM/s1600/akinator.png',
                'https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/93f460de-8276-421d-9163-b5b2fdee6c92/d56rp2o-46708845-6d15-44de-92be-fd664c2d29b6.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzkzZjQ2MGRlLTgyNzYtNDIxZC05MTYzLWI1YjJmZGVlNmM5MlwvZDU2cnAyby00NjcwODg0NS02ZDE1LTQ0ZGUtOTJiZS1mZDY2NGMyZDI5YjYucG5nIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.EfHqHENhD0-tfYgpfLaR1ZFZdATMn2xMP1eaRurdMtk'
            ]
        }
    },
    methods: {
        async getAnswer() {
            this.answer = 'Mmmm...'
            const { answer, image} = await fetch('https://yesno.wtf/api').then( resp => resp.json())
            this.answer = answer === 'yes' ? 'Sí' : 'No'
            this.gif = image
            this.answer === 'Sí' ? this.akinatorStatus = 1 : this.akinatorStatus = 2;
        },
        resetGame() {
            this.isValidQuestion = false;
            if( !value.includes('?') ) return
            this.getAnswer()
            this.isValidQuestion = true;
        }
    },
    watch: {
        question( value) {
            this.isValidQuestion = false;
            if( !value.includes('?') ) return
            this.getAnswer()
            this.isValidQuestion = true;

        },
    }
}
</script>
<style scoped>
    .answer-container {
        display: flex;
        justify-content: center;
        margin-top: 130px;
    }
    .speech-text {
        background: #fff;
        margin: 0 auto;
        width: 200px;
        padding: 40px;
        text-align: center;
        position: relative;
        box-shadow: rgba(0, 0, 0, 0.3) 2px 2px 2px ;
        border-radius: 10px;
    }

    .speech-text:after {
        content: "";
        position: absolute;
        box-shadow: rgba(0, 0, 0, 0.3) 2px 2px 2px ;
        transform: rotate(140deg);
        top: 70px;
        right: 269px;
        border-width: 10px;
        border-style: solid;
        border-color: transparent #FFF #FFF transparent;
    }
    .back {
        border-radius: 5%;
        height: 120px;
        width: 200px;
    }
    .bg-dark {
        background-color: rgba(144, 138, 138, 0.4);
    }
    .indecision-container {
        position: relative;
        z-index: 99;
    }
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }
    p {
        color: rgb(0, 0, 0);
        font-size: 20px;
        margin-top: 0px;
        font-family: 'Arima Madurai'
    }
    h1, h2, span  {
        color: white;
        font-family: 'Arima Madurai'
    }
    
    h2 {
        margin-top: 150px;
    }
</style>