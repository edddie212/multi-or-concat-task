<template>
  <div class="container-fluid">
    <div class="steps text-center">
      <hr :class="step === 1 ? 'active' : ''">
      <hr :class="step === 2 ? 'active' : ''">
      <hr :class="step === 3 ? 'active' : ''">
    </div>
    <div class="container">
      <Wizard :step="step"
              v-model:userChoice="userChoice"
              v-model:choiceValidated="choiceValidated"></Wizard>
    </div>
  </div>
  <div class="buttons container">
    <button @click="preStep"
            :disabled="step === 1"
            type="button"
            class="btn btn-danger">Previous</button>

    <button @click="nextStep"
            :disabled="disableButton()"
            type="button"
            class="btn btn-primary float-end">Next</button>

  </div>
</template>

<script>
import Wizard from "./components/Wizard.vue";
export default {
  name: 'App',
  data() {
    return {
      step: 1,
      userChoice: null,
      choiceValidated: null
    }
  },
  components: {
    Wizard,
  },
  methods: {
    nextStep() {
      this.step++;
    },
    preStep() {
      this.step--;
    },
    disableButton() {
      if (this.step === 3 || !this.userChoice){
        return true;
      }
      if (this.step === 2 && this.choiceValidated === null ){
        return true;
      }

    },
  }
}
</script>

<style scoped>
.steps hr {
  width: 32%;
  display: inline-block;
  margin: 2px;
  background: #21e087;
  height: 0.5rem;
}
.buttons {
  padding: 1rem;
}

.active {
  background: indianred!important;
}


</style>
