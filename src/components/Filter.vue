<template>
  <div class="input-field w-[200px]">
    <select @change="changeSelect">
      <option value="" disabled selected>Choose your filter</option>
      <option value="">All</option>
      <option value="Mens">Mens</option>
      <option value="Gold">Gold</option>
      <option value="Women">Women</option>
      <option value="Gaming">Gaming </option>
    </select>
    <label>Filter</label>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: [String, Number]
  },
  methods: {
    changeSelect(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style lang="scss" scoped></style>