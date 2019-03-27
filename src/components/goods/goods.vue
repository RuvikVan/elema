<template>
  <article>
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" :key="item">
          <p v-show="item.type">{{item.name}}</p>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li v-for="item in goods" class="food-list" :key="item">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item border-1px" :key="food">
              <div class="icon">
                <img width="57" heigh="57" :src="food.icon"/>
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
                <div class="cartcontrol-wrapper">
                  <!--<cartcontrol :food="food"></cartcontrol>-->
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </article>
</template>

<script>
import axios from 'axios'
export default {
  name: 'goods',
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: [],
      listHeight: [],
      scrollY: 0
    }
  },
  created () {
    axios.get('http://118.25.61.61:8080/data/data.json').then((res) => {
      this.goods = res.data.goods
    })
  }
}
</script>

<style scoped>
  article {
    width: 100%;
    display: flex;
    flex-direction: row;
  }

  .menu-wrapper {
    height: 14rem;
    background: #f3f5f7;
  }

  .menu-wrapper ul li {
    display: table;
    width: 1.5rem;
    height: 1rem;
    text-align: center;
  }

  .menu-wrapper ul li p {
    display: table-cell;
    width: 1rem;
    vertical-align: middle;
    font-size: 0.3rem;
    border-top: 0.01rem solid #ffffff;
  }

  .foods-wrapper {
    width: 100%;
  }

  .title {
    display: flex;
    color: rgb(147, 153, 159);
    border-left: 0.1rem solid rgba(7, 17, 27, 0.1);
    background: #f3f5f7;
  }

  .food-item {
    display: flex;
    margin: 0.5rem;
    padding-bottom: 0.5rem;
  }

  .content {
    flex: 1;
    margin-left: 0.4rem;
  }

  .content .name {
    margin: 0.1rem 0 0.1rem 0;
    height: 0.4rem;
    line-height: 0.1rem;
    font-size: 0.4rem;
    color: rgb(7, 17, 27);
  }

  .content .desc, .content .extra {
    line-height: 0.5rem;
    font-size: 0.2rem;
    color: rgb(147, 153, 159)
  }

  .content .extra .count {
    margin-right: 0.2rem
  }

  .content .price {
    font-weight: 700;
    line-height: 0.5rem;
  }

  .content .price .now {
    margin-right: 0.1rem;
    font-size: 0.2rem;
    color: rgb(240, 20, 20);
  }

  .content .price .old {
    text-decoration: line-through;
    font-size: 0.1rem;
    color: rgb(147, 153, 159);
  }

  .cartcontrol-wrapper {
    position: absolute;
    right: 0;
    bottom: 0.1rem;
  }

</style>
