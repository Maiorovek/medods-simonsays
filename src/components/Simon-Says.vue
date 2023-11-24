<template>
    <div class="simon-says">
        <div class="game-buttons">
            <SimonButton 
                color="red" 
                @click.native="userStep(1)" 
                :class="{ 'active': isButtonActive[1] }" 
            />
            <SimonButton 
                color="blue" 
                @click.native="userStep(2)" 
                :class="{ 'active': isButtonActive[2] }" 
            />
            <SimonButton 
                color="green" 
                @click.native="userStep(3)" 
                :class="{ 'active': isButtonActive[3] }" 
            />
            <SimonButton 
                color="orange" 
                @click.native="userStep(4)" 
                :class="{ 'active': isButtonActive[4] }" 
            />
        </div>
        <div class="game-settings">
            <h3> Рануд № {{ curentRound }}</h3>
            <button :disabled="isGameStarted" @click="startGame"> Start </button>
            <div class="game-mode">
                <h4> Выбор сложноси </h4>
                <div>
                    <input 
                        type="radio" 
                        name="mode" 
                        value="1500" 
                        v-model="stepTime" 
                        :disabled="isGameStarted"
                    > 
                    Легкая
                </div>
                <div>
                    <input 
                        type="radio" 
                        name="mode" 
                        value="1000" 
                        v-model="stepTime" 
                        :disabled="isGameStarted"
                    > 
                    Нормальная
                </div>
                <div>
                    <input 
                        type="radio" 
                        name="mode" 
                        value="400" 
                        v-model="stepTime" 
                        :disabled="isGameStarted"
                    > 
                    Сложная
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import SimonButton from './UI/Simon-Button.vue'


export default {
    name: 'SimonSays',

    components: {
        SimonButton,
    },

    data: () => ({
        curentRound: 0,
        order: [],
        userOrder: [],
        isGameStarted: false,
        isGameLost: false,
        step: '',
        isButtonActive: {
            1: false,
            2: false,
            3: false,
            4: false,
        },
        stepTime: 1500,
    }),

    methods: {
        async startGame() {
            if (this.stepTime != 0) {
                this.order = [];
                this.userOrder = [];
                this.curentRound = 0;
                for (let i = 0; i < 20; i++) {
                    this.order.push(Math.floor(Math.random() * 4) + 1);
                }
                this.isGameStarted = true;
                this.step = 'pc';
                this.pcStep();
            } else {
                alert('Выберете сложность')
            }
        },
        
        async userStep(button) {
            if (this.step === 'user' && this.isGameStarted) {
                let audio = new Audio(button + '.mp3');
                audio.play();
                this.userOrder.push(button);

                if (this.userOrder.length === this.curentRound) {
                    for (let i = 0; i < this.curentRound; i++) {
                        if (!(this.userOrder[i] === this.order[i])) {
                            this.isGameStarted = false;
                            alert('Вы проиграли');
                            break;
                        }
                    }
                    if (this.curentRound < 20) {
                        this.step = 'pc'
                        this.pcStep();
                    } else {
                        alert('Вы победили!')
                    }
                }
            }
        },

        timeout(ms) {
            return new Promise(resolve => setTimeout(resolve, ms));
        },

        async pcStep() {
            if (this.isGameStarted) {
                await this.timeout(800)
                for (let i = 0; i <= this.curentRound; i++) {
                    let audio = new Audio(this.order[i] + '.mp3');
                    audio.play();
                    this.isButtonActive[this.order[i]] = true;
                    await this.timeout(this.stepTime / 2);
                    this.isButtonActive[this.order[i]] = false;
                    await this.timeout(this.stepTime / 2);
                }
                this.step = 'user'
                this.userOrder = [];
                this.curentRound++;
            }
        },
    },
}
</script>

<style scoped>
.simon-says {
    display: flex;
    column-gap: 40px;
    justify-content: center;
    
    .game-buttons {
        width: 31vw;
        display: flex;
        flex-wrap: wrap;
        row-gap: 1vw;
        column-gap: 1vw;
    }

    .game-mode {
        display: flex;
        flex-direction: column;
    }
}
</style>