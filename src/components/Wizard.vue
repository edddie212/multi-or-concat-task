<template>
  <div class="wizard">
    <step1 v-if="step === 1" v-model:userChoice="userChoice"></step1>
    <step2 v-else-if="step === 2" :userChoice="userChoice"
           v-model:choiceValidated="choiceValidated"
           v-model:inputOne="inputOne"
           v-model:inputTwo="inputTwo" ></step2>
    <step3 v-else
           v-model:userChoice="userChoice"
           v-model:choiceValidated="choiceValidated"
           v-model:inputOne="inputOne"
           v-model:inputTwo="inputTwo"
    ></step3>
  </div>
</template>

<script>
import step1 from "./step1.vue";
import step2 from "./step2.vue";
import step3 from "./step3.vue";
export default {
  name: "Wizard",
  data(){
    return {
      userChoice: null,
      choiceValidated:null,
      inputOne: null,
      inputTwo: null
    }
  },
  watch: {
    userChoice(value){
      this.$emit('update:userChoice', value)
    },
    choiceValidated() {
      this.$emit('update:choiceValidated', this.choiceValidated)
    }
  },
  emits: ['update:userChoice', 'choiceValidated'],
  props: ['step'],
  components:{
    step1,
    step2,
    step3,
  }
}
</script>

<style scoped>

</style>