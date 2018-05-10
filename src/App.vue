<template>
  <div id="app">
    <v-header :header-seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
     <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
    <shopcart :selectedFoods ="selectedFoods" :deliveryPrice="seller.deliveryPrice"
              :minPrice="seller.minPrice"></shopcart>
  </div>
</template>

<script>
import vHeader from './components/header/header.vue'
import vGoods from './components/goods/goods.vue'
import shopcart from '@/components/shopcart/shopcart'

const ERR_OK = 0
export default {
  name: 'app',
  data () {
    return {
      seller: {
        type: Object
      }
    }
  },
  created () {
    this.$http.get('/api/seller').then(response => {
      if (response.data.errno === ERR_OK) {
        this.seller = response.data.data
      }
    }, response => {
      console.log('error,no data')
    })
  },
  computed: {
    selectedFoods () {
      return this.$store.state.foods
    }
  },
  methods: {
    change (food) {
      this.foos = food
    }
  },
  components: {
    vHeader,
    vGoods,
    shopcart
  }
}
</script>

<style lang="stylus">
 @import "./common/stylus/mixin.styl"
 .tab
   display: flex
   width: 100%
   height: 40px
   line-height: 40px
   border-1px(rgba(7, 17, 27, 0.1))
   .tab-item
     flex: 1
     text-align: center
     & > a
       display: block
       font-size: 14px
       color: rgb(77, 85, 93)
       &.router-link-active
         color: rgb(240, 20, 20)
</style>
