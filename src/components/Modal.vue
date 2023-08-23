<template>
  <div class="flex justify-center w-[100%] items-center h-[100vh] absolute z-[5555] top-0"
    :class="{ hidden: show == false || goods.length <= 0 }" @click.stop="hideModal">
    <div class="shadow fixed w-[100%] h-[100vh] bg-[#bbbbbbc5]"></div>
    <table @click.stop
      class="centered striped py-[20px] w-[70%] fixed top-[150px] max-h-[50px] bg-[white] p-[20px] z-[66] rounded-xl">
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
          <th>TotalPrice</th>
        </tr>
      </thead>

      <tbody>
        <transition-group name="list">
          <tr v-for="good in goods" :key="good.id">
            <td>{{ good.title }}</td>
            <td>{{ good.price.toFixed(2) }}$ (x{{ good.quantity }}) <button class="waves-effect waves-light btn ml-[5px]"
                @click="$emit('add', good)">+</button><button class="waves-effect waves-light btn ml-[5px]"
                @click="$emit('remove', good)">-</button></td>
            <td>{{ (good.quantity * good.price).toFixed(2) }}$ <button class="waves-effect waves-light red btn ml-[15px]"
                @click="$emit('deleteGood', good.id)">Delete</button>
            </td>
          </tr>
        </transition-group>


        <tr class=" border-t-2">
          <td>
            <span class="text-3xl">TotalPrice: {{ totalPrice() }}$</span>
          </td>
        </tr>


      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      required: true
    },
    goods: {
      type: Array,
      required: true
    },

  },
  methods: {
    hideModal() {
      this.$emit('update:show', false)
    },
    totalPrice() {
      return this.goods.reduce((s, item) => {
        return s + item.quantity * item.price
      }, 0).toFixed(2)
    }
  }
}
</script>

<style lang="scss" scoped>
.list-item {
  display: inline-block;
  margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.4s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>