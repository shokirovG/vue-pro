<template>
  <div class="good__list flex flex-wrap gap-[50px] mx-auto justify-center my-[70px] w-[80%]">
    <transition-group name="list">
      <good-item v-if="data.length" class="good__item" v-for="item in data" :key="item.id" :item="item"
        @create="$emit('create', item)" />
      <h1 v-else class="text-2xl">Not Found</h1>
    </transition-group>
  </div>
</template>

<script>
import GoodItem from '@/components/GoodItem.vue'
export default {

  components: {
    GoodItem
  },
  props: {
    data: {
      type: Array,
      required: true
    }
  },
  mounted() {
    console.log(this.data);
  },
}
</script>

<style lang="scss" scoped>
.list-item {
  display: inline-block;
  margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.2s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}</style>