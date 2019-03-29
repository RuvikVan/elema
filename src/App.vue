<template>
  <div id="app">
    <v-header v-bind:seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link :to="{name:'goods'}">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{name:'ratings'}">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{name:'seller'}">商家</router-link>
      </div>
    </div>
    <v-goods v-bind:seller="seller"></v-goods>
<!--    <v-shopcart></v-shopcart>-->
  </div>
</template>

<script>
import header from './components/header/header'
import goods from './components/goods/goods'
import axios from 'axios'

export default {
  name: 'App',
  data () {
    return {
      seller: {}
    }
  },
  components: {
    'v-header': header,
    'v-goods': goods
  },
  created () {
    axios.get('http://118.25.61.61:8080/data/data.json').then((res) => {
      this.seller = res.data.seller
    })
  }
}
</script>

<style>
  @import "./common/css/style.css";
  * {
    margin: 0;
    padding: 0;
  }

  #app .tab {
    display: flex;
    height: 1rem;
    border: 0.05rem solid rgba(7, 17, 27, 0.1);
    line-height: 1rem;
  }

  #app .tab-item {
    text-align: center;
    flex: 1;
  }

  #app .tab-item > a {
    display: block;
    text-decoration: none;
    color: rgb(77, 85, 93);
    font-size: 0.3rem;
  }

  #app .tab-item > a:hover {
    color: rgb(240, 20, 20)
  }
</style>
