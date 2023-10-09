<template>
<div v-if="currentStep === 3">
    <div class="card m-auto">
        <div class="card-header d-flex">
            <my-button
            @click="prevStep"
            class="btn btn-info me-1" 
        >Назад</my-button>

            <h2>Условия</h2>
        </div>
        <div class="card-body">

            <div class="mb-4">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-label="Basic example" style="width: 100%" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100">
                        100%
                    </div>
                </div>
            </div>

            <div class="d-flex justify-content-between border-bottom pb-2 mb-2">
                <div>Сумма займа</div>
                <div>23 000 ₽</div>
            </div>

            <div class="d-flex justify-content-between border-bottom pb-2 mb-2">
                <div>Дата возврата</div>
                <div>25 500 ₽</div>
            </div>

            <div class="d-flex justify-content-between border-bottom pb-2 mb-2">
                <div>Плата за заем</div>
                <div>300 ₽</div>
            </div>

            <div class="d-flex justify-content-between border-bottom pb-2 mb-2">
                <div>Ставка</div>
                <div>0,9 %</div>
            </div>

            <div class="d-flex justify-content-between border-bottom pb-2 mb-2">
                <div>ПСК</div>
                <div>30.04.2020</div>
            </div>
            
            <ul class="my-4">
                <li><a href="#">Проект сертификата дистанционный "Помощник Ц"</a></li>
                <li><a href="#">Памятка использования "Помощник Ц"</a></li>
                <li><a href="#">Согласия на подключение рекуррентного платяжа</a></li>
            </ul>

            <div class="text-center">
  
                <my-button
                    @click="nextStep"
                    class="btn btn-danger"
                >Подписать договор</my-button>
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
    methods: {

    }
}
</script>

<style lang="scss" scoped>
ul,li {
    list-style: none;
    margin: 0;
    padding: 0
}
@media (min-width: 768px) {
    .card {
      width: 25%;
    }
  }
</style>