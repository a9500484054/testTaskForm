<template>
<div v-if="currentStep === 2">
    <div class="card  m-auto">
        <div class="card-header">
            <my-button
                @click="prevStep"
                class="btn btn-info me-1" 
            >назад</my-button>
        </div>
        <div class="card-body">
            <div class="text-center">
                <h2>Подверждения удаленной индификации</h2>
                <p>Мы отправили вам SMS c кодом на ваш номер телефона</p>
                <p v-show="isVisibleCode">Ваш код {{ code }} </p>
            </div>

            <div class="mb-3">
                <label for="code-sms">Код</label>
                <my-input 
                    :disabled="inputeDisabled"
                    id="code-sms"
                    v-model="codeSMS"
                    placeholder="Введите код из смс"
                />
                <p class="text-center text-danger"> {{ textError }} </p>
            </div>

            <div class="text-center mb-3">
                <my-button
                    :disabled="codeSMS === ''"
                    v-show="isVisibleCheckCode"
                    @click="checkCode"
                    class="btn btn-danger" 
                >Проверить код</my-button>
            </div>
            <div class="text-center mb-3">
                <my-button
                    v-show="isVisibleSendCode"
                    @click="startTimer"
                    class="btn btn-danger" 
                >Отправить код</my-button>
            </div>


            <div class="text-center" v-show="isVisibleBlockTimer">
                <p>отправить код повторно через</p>
                <p>{{ seconds }}</p>
            </div>
            

            <div class="text-center" v-show="isVisibleNextStep">

                <my-button
                    @click="nextStep"
                    class="btn btn-danger" 
                >Продолжить</my-button>
            </div>


        </div>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            codeSMS: '',
            seconds: 0,
            isVisibleSendCode: true,
            isVisibleCheckCode: false,
            isVisibleBlockTimer: false,
            isVisibleCode: false,
            inputeDisabled: false,
            isVisibleNextStep: false,
            code: null,
            timer: null,
            textError: '',
        } 
    }, 
    props: {
        nextStep: {
            type: Function,
            required: true
        },
        prevStep: {
            type: Function,
            required: true
        },
        currentStep: {
            type: Number,
            required: true
        },
    },
    methods: {
        startTimer() {
            this.isVisibleCode = false;
            this.code = this.generateFourCode();
            this.isVisibleSendCode = false;
            this.isVisibleCheckCode = true;
            this.isVisibleBlockTimer = true;
            this.showCode();

            this.seconds = 10

            this.timer = setInterval(() => {
            this.seconds--;

            if (this.seconds >= 1) {
                this.timerValue = this.seconds;
            } else {
                clearInterval(this.timer);
                this.isVisibleSendCode = true;
                this.isVisibleBlockTimer = false;
            }
            
            }, 1000);
        },
        checkCode() {
            if (+this.codeSMS === this.code) {
                this.textError = ''
                this.isVisibleSendCode = false;
                this.isVisibleCheckCode = false;
                this.isVisibleBlockTimer = false;
                this.inputeDisabled = true;
                this.isVisibleNextStep = true;
                this.code = 'принят'
                clearInterval(this.timer)
            } else {
                this.textError = 'код не верный'
            }
        },
        showCode() {
            setTimeout(() => {
                this.isVisibleCode = true;
            }, 2000)
        },
        generateFourCode() {
            return Math.floor(Math.random() * 9000) + 1000;
        }
    }
}
</script>

<style lang="scss" scoped>
@media (min-width: 768px) {
    .card {
      width: 25%;
    }
  }
</style>