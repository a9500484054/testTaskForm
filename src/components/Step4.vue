<template>
<div v-if="currentStep === 4">
    <div class="card  m-auto">
        <div class="card-header">
            <h2>Проверка данных</h2>
        </div>
        <div class="card-body">
            <div class="mb-3">
                <div class="loader m-auto"></div>
            </div>

            <div class="mb-3 text-center">
                <p>Проверка Ваших данных!</p>
                <p>Это займет до 30 минут!</p>
            </div>


        </div>
    </div>
</div>
</template>

<script>
export default {
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
    watch: {
        currentStep(newValue) {
            if (newValue === 4) {
                setTimeout(()=> {
                    this.nextStep();
                }, 3000)
            }
        }
    },
    methods: {
        
    }
}
</script>

<style lang="scss" scoped>
    .loader {
        width: 48px;
        height: 48px;
        border-radius: 50%;
        position: relative;
        animation: rotate 1s linear infinite
    }
    .loader::before , .loader::after {
        content: "";
        box-sizing: border-box;
        position: absolute;
        inset: 0px;
        border-radius: 50%;
        border: 5px solid #FFF;
        animation: prixClipFix 2s linear infinite ;
    }
    .loader::after{
        transform: rotate3d(90, 90, 0, 180deg );
        border-color: #FF3D00;
    }

    @keyframes rotate {
        0%   {transform: rotate(0deg)}
        100%   {transform: rotate(360deg)}
    }

    @keyframes prixClipFix {
        0%   {clip-path:polygon(50% 50%,0 0,0 0,0 0,0 0,0 0)}
        50%  {clip-path:polygon(50% 50%,0 0,100% 0,100% 0,100% 0,100% 0)}
        75%, 100%  {clip-path:polygon(50% 50%,0 0,100% 0,100% 100%,100% 100%,100% 100%)}
    }
    @media (min-width: 768px) {
        .card {
          width: 25%;
        }
      }
</style>