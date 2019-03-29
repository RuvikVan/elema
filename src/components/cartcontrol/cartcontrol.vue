<template>
  <div class="cartcontrol">
    <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click="decreaseCart"></div>
    <div class="cart-count" v-show="food.count>0"> {{ food.count }}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  name: 'cartcontrol',
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart () {
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
    },
    decreaseCart () {
      if (this.food.count) {
        this.food.count--
      }
    }
  }
}
</script>

<style scoped>

  .cartcontrol {
  }

  .cart-decrease {
    display: inline-block;
    font-size: 0.5rem;
  }

  .cart-count {
    display: inline-block;
    font-size: 0.5rem;
    margin-left: 0.3rem;
  }

  .cart-add {
    display: inline-block;
    font-size: 0.5rem;
    margin-left: 0.3rem;
  }
</style>
