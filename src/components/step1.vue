<template>
  <div class="buttons">
    <div class="row items-center aligns-items-center justify-content-center">
        <button @click="SetUserChoice" :class="userChoice === 'concat' ? 'btn-primary':'btn-secondary'" class="btn col-5 m-2" value="concat" >
          Concat
        </button>
        <button @click="SetUserChoice" :class="userChoice === 'multiply' ? 'btn-primary':'btn-secondary'" class="btn col-5 m-2" value="multiply" >
          Multiply
        </button>
    </div>

  </div>
</template>

<script>
export default {
  name: "step1",
  props: ['userChoice'],
  emits: ['update:userChoice'],
  methods: {
    SetUserChoice(value) {
      this.$emit('update:userChoice', value.target.value)
    },
  }

}
</script>

<style scoped>



</style>