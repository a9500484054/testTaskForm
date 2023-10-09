<template>
  <div>
    <h1 class="text-center mb-5">Заявка на кредит</h1>

    <div>

        <!-- Шаг 1 -->
        <Step1 
          :current-step="currentStep" 
          :next-step="nextStep" 
        ></Step1>

        <!-- Шаг 2 -->
        <Step2 
          :current-step="currentStep" 
          :prev-step="prevStep" 
          :next-step="nextStep" 
        ></Step2>
        
        <!-- Шаг 3 -->
        <Step3
          :current-step="currentStep" 
          :prev-step="prevStep"
          :next-step="nextStep" 
        ></Step3>
        
        <!-- Шаг 4 -->
        <Step4
          :current-step="currentStep" 
          :prev-step="prevStep"
          :next-step="nextStep" 
        ></Step4>
        
        <!-- Шаг 5 -->
        <Step5
          :current-step="currentStep" 
          :update-step="updateStep"
        ></Step5>



    </div>
  
  </div>
</template>

<script>
import Step1 from '@/components/Step1.vue';
import Step2 from '@/components/Step2.vue';
import Step3 from '@/components/Step3.vue';
import Step4 from '@/components/Step4.vue';
import Step5 from '@/components/Step5.vue';


export default {
  components: { Step1,Step2,Step3,Step4,Step5 },
  data() {
    return {
      currentStep: 1
    }
  },
  methods: {
    nextStep() {
      if (this.currentStep < 5) {
        this.currentStep++;
      }
    },
    prevStep() {
      if (this.currentStep > 1) {
        this.currentStep--;
      }
    },
    updateStep(step) {
      this.currentStep = step;
    },
  },

  
}
</script>

<style lang="scss">

</style>
