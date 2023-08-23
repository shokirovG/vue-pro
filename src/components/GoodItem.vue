<template>
  <div class="card w-[250px] p-[10px]">
    <div class="card-image w-[200px] h-[200px]">
      <img :src="item.image" class="h-[200px]">

    </div>
    <div class="card-content">
      <span class="card-title">{{ item.title.slice(0, 10) }}...</span>
      <p>{{ item.description.slice(0, 60) }}...</p>
    </div>
    <div class="card-action">
      <h2 class="text-2xl ">{{ item.price }}$</h2>
      <a class="waves-effect waves-light btn mt-[10px]" @click="$emit('create', item)">Buy</a>
    </div>
  </div>
</template>

<script>
export default {
  data() {

  },
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  mounted() {

  },
  methods: {

  }
}
</script>

<style lang="scss" scoped></style>