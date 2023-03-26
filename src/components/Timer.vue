<script>
export default {
    data() {
        return {
            seconds: 0,
            minutes: 0,
            hours: 0,
            timer: null,
            go: false
        }
    },
    methods: {
        startStop(){
            if(!this.go){
                this.startTimer()
            }else{
                this.stopTimer()
            }
        },
        startTimer(){
            this.go = true
            this.timer = setInterval(() => {
                this.seconds++
                if(this.seconds === 60){
                    this.seconds = 0;
                    this.minutes++;
                }
                else if(this.minutes === 60){
                    this.minutes = 0;
                    this.hours++
                }
            }, 1000);
        },
        stopTimer(){
            this.go = false
            clearInterval(this.timer)
        },
        resetTimer(){
            this.stopTimer();

            this.seconds = 0;
            this.minutes = 0;
            this.hours = 0;
        }
    }
}
</script>

<template>
    <div class="timer-wrapper">
        <div class="timer-wrapper__header">
            <span class="timer-wrapper__header__span">
                {{ (hours > 0 ? (hours < 10 ? '0' + hours : hours) + ' : ': '') + (minutes > 0 ? (minutes < 10 ? '0' + minutes : minutes) + ' : ': '') + (seconds < 10 ? '0' + seconds : seconds) }}
            </span>
        </div>
        <div class="timer-wrapper__footer">
            <button class="timer-wrapper__footer__start-pause" @click="startStop">
                <img v-if="!go" src="/svg/start.svg/" alt="Старт">
                <img v-else src="/svg/pause.svg/" alt="Пауза">
            </button>
            <button class="timer-wrapper__footer__stop" @click="resetTimer"></button>
        </div>
    </div>
</template>

<style lang='scss' scoped>
.timer-wrapper {
    width: 225px;
    height: 120px;
    background-color: #696969;

    &__header {
        height: 60px;
        display: flex;
        justify-content: center;
        align-items: center;

        &__span {
            font-size: 22px;
            line-height: 21px;
            color: #9E9E9E;
        }
    }
    &__footer{
        border-top: 1px solid #9E9E9E;
        height: 59px;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 48px;
        &__start-pause{
            width: 17px;
            height: 20px;
            border: none;
            background-color: transparent;
            padding: 0;
            cursor: pointer;
        }
        &__stop{
            width: 20px;
            height: 20px;
            border: none;
            background-color: #9E9E9E;
            cursor: pointer;
        }
    }

}
</style>