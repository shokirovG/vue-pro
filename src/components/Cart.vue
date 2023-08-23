<template>
  <div class="fixed right-[50px] top-[100px] z-[99] ">
    <i class="medium material-icons text-[10px]  cursor-pointer   ml-[15px]">add_shopping_cart </i>
    <p v-if="empty == true" class="text-[red]">Cart is Empty!</p>
  </div>
</template>

<script>
export default {
  props: {
    empty: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped></style>