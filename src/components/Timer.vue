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
        startStop() {
            if (!this.go) {
                this.startTimer()
            } else {
                this.stopTimer()
            }
        },
        startTimer() {
            this.go = true
            this.timer = setInterval(() => {
                this.seconds++
                if (this.seconds === 60) {
                    this.seconds = 0;
                    this.minutes++;
                }
                else if (this.minutes === 60) {
                    this.minutes = 0;
                    this.hours++
                }
            }, 1000);
        },
        stopTimer() {
            this.go = false
            clearInterval(this.timer)
        },
        resetTimer() {
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
            <span :class="['timer-wrapper__header__span', { 'timer-wrapper__header__span_white': go }]">
                {{ (hours > 0 ? (hours < 10 ? '0' + hours : hours) + ':' : '') + (minutes > 0 ? (minutes < 10 ? '0' +
                    minutes : minutes) + ':' : '') + (seconds < 10 ? '0' + seconds : seconds) }} </span>
        </div>
        <div :class="['timer-wrapper__footer', { 'timer-wrapper__footer_whiter-border': go }]">
            <button class="timer-wrapper__footer__start-pause" @click="startStop">
                <svg v-if="!go" alt="Старт" width="17" height="20" viewBox="0 0 17 20" fill="none"
                    xmlns="http://www.w3.org/2000/svg">
                    <path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E" />
                </svg>
                <svg v-else alt="Пауза" width="10" height="20" viewBox="0 0 10 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect x="7" width="3" height="20" fill="#FFFFFF" />
                    <rect width="3" height="20" fill="#FFFFFF" />
                </svg>
            </button>
            <button :class="['timer-wrapper__footer__stop', {'timer-wrapper__footer__stop_white': go}]" @click="resetTimer"></button>
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

            &_white {
                color: #FFFFFF;
            }
        }
    }

    &__footer {
        border-top: 1px solid #9E9E9E;
        height: 59px;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 48px;

        &_whiter-border {
            border-top: 1px solid #FFFFFF;
        }

        &__start-pause {
            width: 17px;
            height: 20px;
            border: none;
            background-color: transparent;
            padding: 0;
            cursor: pointer;
        }

        &__stop {
            width: 20px;
            height: 20px;
            border: none;
            background-color: #9E9E9E;
            cursor: pointer;
            &_white{
                background-color: #FFFFFF;
            }
        }
    }

}
</style>