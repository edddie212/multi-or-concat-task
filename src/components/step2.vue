<template>

  <div class="container d-flex items-center aligns-items-center justify-content-center">
    <p class="user-choice ">
      <span :class="userChoice === 'concat' ? 'active-choice' : ''">C</span>
      /
      <span :class="userChoice === 'multiply' ? 'active-choice' : ''">M</span>
    </p>

  </div>

  <p v-if="this.error.length > 0" class="text-danger">Error: {{this.error}}</p>
  <p v-if="this.emptyInputError.length > 0" class="text-danger">Error: {{this.emptyInputError}}</p>

  <input class="form-control form-control-lg mb-3"
         id="input-1"
         @input="checkInputs"
         type="text"
         :placeholder="this.userChoice === 'multiply' ? 'Please enter a number' : 'Enter letters or sentence'">
  <input class="form-control form-control-lg"
         id="input-2"

         @input="checkInputs"
         type="text"
         :placeholder="this.userChoice === 'multiply' ? 'Please enter a number' : 'Enter letters or sentence'">

</template>

<script>
export default {
  name: "step2",
  props: ['userChoice', 'choiceValidated'],
  emits: ['update:inputOne', 'update:inputTwo','update:choiceValidated'],
  data() {
    return {
      error:'',
      emptyInputError: ''
    }
  },
  methods: {
    checkInputs() {
      const input1 = document.getElementById('input-1').value;
      const input2 = document.getElementById('input-2').value;
      if(input1.length <= 0 || input2.length <= 0) {
        this.$emit('update:choiceValidated', null)
        this.emptyInputError = 'Please enter a value';
      } else {
        //Number validation
        if(this.userChoice === 'multiply') {
          const matchesMultiInput1 = /^\d+$/.exec(input1);
          const matchesMultiInput2 = /^\d+$/.exec(input2);
          if(matchesMultiInput1 != null && matchesMultiInput2 != null){
            this.$emit('update:inputOne', input1.trim());
            this.$emit('update:inputTwo', input2.trim());
            this.$emit('update:choiceValidated', true)
            this.error = '';
            this.emptyInputError = '';
          } else {
            this.error = 'Please enter a number format only';
            this.emptyInputError = '';
            this.$emit('update:choiceValidated', null)
          }
        }
        //String validation
        if(this.userChoice === 'concat') {
          const matchesConcatInput1 =  /^[a-z A-Z]+$/.exec(input1);
          const matchesConcatInput2 =  /^[a-z A-Z]+$/.exec(input2);
          if(matchesConcatInput1 != null && matchesConcatInput2 != null){
            this.$emit('update:inputOne', input1.trim());
            this.$emit('update:inputTwo', input2.trim());
            this.$emit('update:choiceValidated', true)
            this.error = '';
            this.emptyInputError = '';
          } else {
            this.error = 'Please enter a string(letters/sentence/word) format only';
            this.emptyInputError = '';
            this.$emit('update:choiceValidated', null)
          }

        }
      }

    },
  },
  mounted() {
    this.$emit('update:inputOne','');
    this.$emit('update:inputTwo', '');
    this.$emit('update:choiceValidated', null)
  }
}
</script>

<style scoped>
.user-choice {
  border: 2px solid;
  width: 40%;
  text-align: center;
  padding: 0.3rem;
  margin-top: 0.4rem;
  border-radius: 25px;
}
.active-choice {
  background: #2fcfc0;
  padding: 3px;
  border-radius: 21%;
}
</style>