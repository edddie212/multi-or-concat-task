<template>
  <div class="container d-flex items-center aligns-items-center justify-content-center">
    <div class="card" >
      <div class="card-body text-center">
        <h5  class="card-title ">Your Result</h5>
        <p class="card-text">{{this.result}}</p>
        <div class="d-flex items-center aligns-items-center justify-content-center">
          <button
              @click="reset"
              type="button"
              class="mt-3 mb-3 btn btn-primary float-end">Reset</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "step3",
  props: ['inputOne', 'inputTwo', 'userChoice', 'choiceValidated'],
  data(){
    return {
      result: ''
    }
  },
  methods: {
    reset() {
      window.location = '/';
    }
  },
  mounted() {
    if (this.userChoice === 'multiply'){
      this.result  = parseInt(this.inputOne)*parseInt(this.inputTwo);
    } else {
      this.result = this.inputOne+this.inputTwo;
    }
  }
}
</script>

<style scoped>
.card {
  width: 18rem;
  margin: 4vh 0vh;
}

.card-title {
  font-size: 2rem;
}

.card-text {
  font-size: 1.8rem;
}
</style>