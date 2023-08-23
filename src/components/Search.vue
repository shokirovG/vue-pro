<template>
  <form class="col s12 flex justify-center items-center">

    <div class="input-field w-[300px]">
      <input placeholder="Search by title" id="first_name" type="text" class="validate" :value="modelValue"
        @input="changeValue">

    </div>



  </form>
</template>

<script>
export default {
  props: {
    modelValue: [String, Number]
  },
  methods: {
    changeValue(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style lang="scss" scoped></style>