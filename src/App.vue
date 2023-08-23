<template>
  <div class="app">


    <Header />
    <div class="flex  items-center justify-center gap-[50px] mt-[30px]">
      <Search v-model="searchPost" />
      <Filter v-model="searchPost" />
    </div>

    <Cart @click="showHideCart" :empty="empty" />
    <Modal v-model:show="modal" :goods="goods" @add="addToCart" @remove="removeGood" @deleteGood="deleteGood" />
    <good-list v-if="!loading" :data="searchedPosts" @create="addToCart" />
    <loader v-else-if="loading" />
    <Footer />
  </div>
</template>

<script>
import axios from 'axios';
import { GoodList, Loader, Header, Footer, Cart, Modal, Search, Filter } from '@/components/index'
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';
export default {
  components: {
    GoodList, Loader, Header, Footer, Cart, Modal, Search, Filter
  },
  data() {
    return {
      data: [],
      limit: 10,
      page: 0,
      loading: true,
      modal: false,
      goods: [],
      empty: false,
      searchPost: ''
    }
  },
  methods: {
    async fetching() {
      const request = await axios.get('https://fakestoreapi.com/products')
      this.data = request.data

      this.page = Math.ceil(request.data.length / this.limit)
      this.loading = false
      document.body.style.overflow = 'visible'

    },
    showHideCart() {
      if (this.goods.length <= 0) {
        this.empty = true
      }
      else {
        this.empty = false
      }

      if (this.goods.length > 0) {
        this.modal = !this.modal
      }
      else {
        this.modal = false
      }

    },
    addToCart(good) {

      const findItem = this.goods.findIndex(el => el.id === good.id)
      console.log(findItem);
      if (findItem < 0) {
        good = { ...good, quantity: 1 }
        this.goods.push(good)
      }
      else {
        const newGoods = this.goods.map(elem => {
          if (elem.id === good.id) {
            return {
              ...good,
              quantity: elem.quantity + 1
            }
          }
          else {
            return elem
          }
        })
        this.goods = newGoods
      }
      if (this.goods.length <= 0) {
        this.empty = true
      }
      else {
        this.empty = false
      }

      toast.success(`Buyed ${good.title}`, {
        autoClose: 1000,
      });
    },
    removeGood(good) {


      const newGoods = this.goods.map(elem => {
        if (elem.id === good.id) {
          return {
            ...good,
            quantity: elem.quantity > 1 ? elem.quantity - 1 : elem.quantity
          }
        }
        else {
          return elem
        }
      })
      this.goods = newGoods
      if (good.quantity > 1) {
        toast.error(`Removed ${good.title}`, {
          autoClose: 1000,
        }); // ToastOptions
      }
    },
    deleteGood(id) {
      this.goods.forEach(el => {
        if (el.id === id) {
          toast.dark(`deleted ${el.title}`, {
            autoClose: 1000,
          }); // ToastOptions
        }
      })
      this.goods = this.goods.filter(el => el.id !== id)
      if (this.goods.length < 1) {
        this.modal = false
      }

    },


  },
  mounted() {
    this.fetching()

  }, computed: {
    searchedPosts() {
      console.log('searched');
      return this.data.filter(el => el.title.toLowerCase().includes(this.searchPost.toLocaleLowerCase()))
    }
  }
}
</script>

<style >
body {
  overflow: hidden;
}

.app {
  width: 100%;
}

* {
  margin: 0;
  padding: 0;
}
</style>