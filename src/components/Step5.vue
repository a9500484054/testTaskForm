<template>
<div v-if="currentStep === 5">
    <div class="card  m-auto">
        <div class="card-header">
            <h2>Договор подписан</h2>
        </div>
        <div class="card-body">
            <div class="check-line  m-auto">
                <i class="ri-check-line fs-18"></i> 
            </div>

            <div class="text-center">
                <p>Договор подписан.</p>
                <p>Ожидайте поступления денежных средств.</p>
            </div>
            
            
            <div class="text-center">
                <my-button
                    @click="updateStep(1)"
                    class="btn btn-success" 
                >перейти на шаг 1</my-button>
            </div>



        </div>
    </div>
</div>
</template>

<script>
export default {
    props: {
        updateStep: {
            type: Function,
            required: true
        },
        currentStep: {
            type: Number,
            required: true
        },
    },
    methods: {
        
    }
}
</script>

<style lang="scss" scoped>
    .check-line {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 4em;
        height: 4em;
        border: 1px solid #000;
        border-radius: 50%;
        i {
            font-size: 26px;
        }
    }
    @media (min-width: 768px) {
        .card {
          width: 25%;
        }
      }
</style>