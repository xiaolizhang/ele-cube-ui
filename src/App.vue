<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <tab :tabs="tabs"></tab>
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header'
import Tab from 'components/tab/tarBar'
import Goods from 'components/goods/goods'
import Seller from 'components/seller/seller'
import Ratings from 'components/ratings/ratings'
import { getSeller} from "./api";


export default {
  name: 'app',
  data(){
    return {
      seller:{}
    }
  },
  components: {
    VHeader,
    Tab,
    Goods,
    Seller,
    Ratings
  },
  created() {
    this._getSeller()
  },
  computed: {
    tabs() {
      return [
        {
          label:'商品',
          component:Goods,
          data:{seller:this.seller}
        },
        {
          label:'评价',
          component:Ratings,
          data:{seller:this.seller}
        },
        {
          label:'商家',
          component:Seller,
          data:{seller:this.seller}
        }
      ]
    }
  },
  methods:{
    _getSeller(){
      getSeller().then((seller) => {
        this.seller = seller
      })
    }
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
