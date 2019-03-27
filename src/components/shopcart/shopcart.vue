<template>
  <footer>
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highlight':totalCount>0}">
            <span class="icon-shopping_cart" :class="{'highlight':totalCount>0}"></span>
          </div>
          <div class="num" v-show="totalCount>0">{{ totalCount }}</div>
        </div>
        <div class="price" :class="{'highlight':totalPrice>0}">￥{{totalPrice}}元</div>
        <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="content-right">
        <div class="pay" :class="payClass">{{ payDesc }}</div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'shopcart',
  props: {
    selectFoods: {
      type: Array,
      default () {
        return [
          {
            price: 123,
            count: 12
          }
        ]
      }
    },
    deliveryPrice: {
      type: Number,
      default: 9
    },
    minPrice: {
      type: Number,
      default: 0
    }
  },
  computed: {
    totalCount () {
      let count = 0
      this.selectFoods.forEach((food) => {
        count += food.count
      })
      return count
    },
    totalPrice () {
      let sum = 0
      this.selectFoods.forEach((food) => {
        sum += food.price * food.count
      })
      return sum
    },
    payDesc () {
      if (this.totalPrice === 0) {
        return `¥${this.minPrice}元起送`
      } else if (this.totalPrice < this.minPrice) {
        let diff = this.minPrice - this.totalPrice
        return `还差¥${diff}元起送`
      } else {
        return '去结算'
      }
    },
    payClass () {
      if (this.totalPrice < this.minPrice) {
        return 'not-enough'
      } else {
        return 'enough'
      }
    }
  }
}
</script>

<style scoped>
  @import "../../common/css/style.css";

  footer {
    position: fixed;
    left: 0;
    bottom: 0;
    right: 0;
    z-index: 50;
    width: 100%;
    height: 1.5rem;
    background: #000;
  }

  .content {
    display: flex;
    background: #141d27;
    font-size: 0;
    color: rgba(255, 255, 255, 0.4);
  }

  .content-left {
    flex: 1;
  }

  .content-left .logo-wrapper {
    display: inline-block;
    vertical-align: top;
    position: relative;
    top: -0.5rem;
    margin: 0 0.3rem;
    padding: 0.3rem;
    width: 1rem;
    height: 1rem;
    border-radius: 50%;
    background: #141d27;
  }

  .content-left .logo-wrapper .logo {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    text-align: center;
    background: #2b343c;
  }

  .content-left .highlight:nth-child(1) {
    color: white;
    background: rgb(0, 160, 220)
  }

  .content-left .highlight:nth-child(2) {
    color: #ffffff
  }

  .icon-shopping_cart {
    line-height: 1rem;
    font-size: 0.5rem;
    color: #80858a;
  }

  .num {
    position: absolute;
    top: 0;
    right: 0;
    width: 0.8rem;
    height: 0.4rem;
    text-align: center;
    border-radius: 1rem;
    font-size: 0.1rem;
    font-weight: 700;
    color: #ffffff;
    background: rgb(240, 20, 20);
    /*box-shadow: 0px 4px 8px 0 rgba(0, 0, 0, 0.4);*/
  }

  .price {
    display: inline-block;
    height: 100%;
    vertical-align: top;
    padding-right: 0.1rem;
    line-height: 1.5rem;
    box-sizing: border-box;
    border-right: 0.05rem solid rgba(255, 255, 255, 0.1);
    font-size: 0.3rem;
    font-weight: 700;
  }

  .desc {
    height: 100%;
    display: inline-block;
    vertical-align: top;
    margin-left: 0.4rem;
    line-height: 1.5rem;
    font-size: 0.3rem;
  }

  .content-right {
    width: 3rem;
  }

  .content-right .pay {
    height: 1.5rem;
    line-height: 1.5rem;
    text-align: center;
    font-size: 0.4rem;
    font-weight: 700;
    background: #2b333b;
  }

  .content-right .not-enough {
    background: #2b333b;
  }

  .content-right .enough {
    background: #00b43c;
    color: #fff;
  }
</style>
