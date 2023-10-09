<template>
<div v-if="currentStep === 1">
    <div class="card m-auto">
        <div class="card-header">
            <h2>Шаг 1: Личные данные</h2>
        </div>

        
        <div class="card-body">
            
            <div class="mb-4">
                <my-bar>25%</my-bar>
            </div>

            <div class="row">
                <div class="col-md-6">
                    <div class="mb-3">
                        <input 
                            v-model="form.firstName"
                            ref="firstName"
                            type="text" 
                            class="form-control" 
                            @input="checkInput"
                            placeholder="Имя*"
                        >
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="mb-3">
                        <input 
                            v-model="form.lastName"
                            ref="lastName"
                            type="text" 
                            class="form-control" 
                            @input="checkInput"
                            placeholder="Фамилия*"
                        >
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="mb-3">
                        <input 
                            v-model="form.middleName"
                            ref="middleName"
                            type="text" 
                            class="form-control" 
                            @input="checkInput"
                            placeholder="Отчество*"
                        >
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="mb-3">
                        <input 
                            v-model="form.dateOfBirth"
                            ref="dateOfBirth"
                            type="text" 
                            class="form-control" 
                            @input="checkInput"
                            placeholder="Дата рождения*"
                        >
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="mb-3">
                        <input 
                            v-model="form.birthCountry"
                            ref="birthCountry"
                            type="text" 
                            class="form-control" 
                            @input="checkInput"
                            placeholder="Страна место рождения*"
                        >
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="mb-3">
                        <input 
                            v-model="form.email"
                            ref="email"
                            type="text" 
                            class="form-control" 
                            @input="checkInput"
                            placeholder="Email"
                        >
                    </div>
                </div>
            </div>

            <div class="text-center">
                <div>Заполнить через</div>
                <a href="#">
                    <img src="https://russian7.ru/wp-content/uploads/2022/02/2-12.jpg" alt="" width="200">
                </a>
            </div>

            <div class="mb-3 d-flex align-items-baseline px-5">
                <input
                    v-model="agreements"
                    id="agreements"
                    type="checkbox" 
                    class="me-2" 
                >
                <label for="agreements">Даю согласия на обработку личных данных и подписание документов в электронном виде</label>
            </div>

            <div class="text-center mb-4">
                <my-button
                    @click="checkForm"
                    class="btn btn-danger" 
                    type="button"
                >Продолжить</my-button>
            </div>


            <p class="text-center text-danger">{{ textError }}</p>
            <p class="text-center text-danger">{{ textAgreements }}</p>

        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios';
import mockServer from '@/mock/myserver.js'
export default {
    data() {
        return {
            form: {
                firstName: "",
                lastName: "",
                middleName: "",
                dateOfBirth: "",
                birthCountry: "",
                email: ""
            },
            agreements: false,
            textError: '',
            textAgreements: '',
            hasError: false,
            formChanged: false
        }
    },
    props: {
        nextStep: {
            type: Function,
            required: true
        },
        currentStep: {
            type: Number,
            required: true
        },
    },
    methods: {
        checkForm() {
            this.hasError = false;

            for (let field in this.form) {
                if (this.form[field] === '') {
                    this.$refs[field].classList.add('is-invalid');
                    this.$refs[field].classList.remove('is-valid');
                    this.hasError = true;
                } else {
                    this.$refs[field].classList.add('is-valid');
                    this.$refs[field].classList.remove('is-invalid');
                }
            }

            this.textError = this.hasError ? 'Данные заполнены не корректно' : '';
            this.textAgreements = !this.agreements ? 'Необходимо дать согласится на обработку данных' : '';

            if (!this.hasError && this.agreements) {
                const data = {
                    firstName: this.form.firstName,
                    lastName: this.form.lastName,
                    middleName: this.form.middleName,
                    dateOfBirth: this.form.dateOfBirth,
                    birthCountry: this.form.birthCountry,
                    email: this.form.email
                };

                if(this.formChanged) {
                    this.getDataForm(data)
                    this.formChanged = false;
                } else {
                    this.nextStep()
                }
                
            }
            console.log(this.formChanged)

        },
        checkInput() {
            this.formChanged = true;
        },
        async getDataForm(data) {
            try {
                const headers = {
                    'Content-Type': 'application/json',
                    'Authorization': 'Bearer 12345'
                };

                const response = await axios.post('/api/data', data, { headers });
                
                console.log(response);
                console.log(response.data);
                this.nextStep()

            } catch (error) {
                console.error(error.response.data.error);
                this.textError = 'данные не отправлены'
            }
        }
    },
    
}
</script>

<style lang="scss" scoped>
    @media (min-width: 768px) {
        .card {
        width: 25%;
        }
    }
</style>