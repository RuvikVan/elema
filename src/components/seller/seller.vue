<template>
  <article>
    <div class="first-content">
      <div class="first-content-top">
        <span>{{ seller.name }}</span>
        <div class="first-content-top-c">
          <v-star :size="24" :score="seller.foodScore" class="qwe1"></v-star>
          <span>({{seller.ratingCount}})</span>
          <span>月售{{seller.sellCount}}单</span>
        </div>
      </div>
      <div class="first-content-bottom">
        <div>
          <h2>起送价</h2>
          <span class="stress">{{seller.minPrice}}</span>元
        </div>
        <div>
          <h2>商家配送</h2>
          <span class="stress">{{seller.deliveryPrice}}</span>元
        </div>
        <div>
          <h2>平均配送时间</h2>
          <span class="stress">{{seller.deliveryTime}}</span>分钟
        </div>
      </div>
    </div>
    <div class="second-content">
      <div>
        <h1 class="title">公告与活动</h1>
        <p class="content">{{seller.bulletin}}</p>
      </div>
      <ul v-if="seller.supports" class="supports">
        <li class="support-item" v-for="(item,index) in seller.supports" :key="item">
<!--          <span class="icon" :class="classMap[seller.supports[index].type]"></span>-->
          <span class="text">{{seller.supports[index].description}}</span>
        </li>
      </ul>
    </div>
    <div class="third-content">
      <h1 class="title">商家实景</h1>
      <div class="pic-wrapper" ref="picWrapper">
        <ul class="pic-list" ref="picList">
          <li class="pic-item" v-for="pic in seller.pics" :key="pic">
            <img :src="pic" width="120" height="90">
          </li>
        </ul>
      </div>
    </div>
    <div class="fourth-content">
      <h1 class="title border-1px">商家信息</h1>
      <ul>
        <li class="info-item" v-for="info in seller.infos" :key="info">{{info}}</li>
      </ul>
    </div>
  </article>
</template>
<script>
import star from '../star/star'

export default {
  name: 'seller',
  props: {
    seller: {
      type: Object
    }
  },
  components: {
    'v-star': star
  }
}
</script>

<style scoped>
  article {
    display: flex;
    flex-direction: column;
  }

  .first-content {
    width: 100%;
  }

  .first-content-top-c {
    margin-top: 0.4rem;
    margin-left: 0.2rem;
  }

  .first-content-top span:nth-child(1) {
    font-size: 0.4rem;
    display: inline-block;
    margin-top: 0.4rem;
    margin-left: 0.2rem;
  }

  .qwe1 {
    display: inline-block;
  }

  .first-content-bottom {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    margin-top: 0.5rem;
  }

  .first-content-bottom span {
    font-size: 0.6rem;
  }

  .first-content-bottom div:nth-child(1) {
    margin-left: 1rem;
  }

  .first-content-bottom div:nth-child(2) {
    margin-left: 2rem;
  }

  .first-content-bottom div:nth-child(3) {
    margin-left: 1rem;
  }

  .title {
    margin-top: 0.2rem;
    margin-left: 0.2rem;
  }

  .support-item {
    padding: 0.4rem;
  }

  .content {
    color: red;
    margin: 0.5rem;
  }

  .second-content {
    border-top: 1rem solid gray;
    margin-top: 0.5rem;
  }

  .support-item {
    border-top: 0.1rem solid lightgrey;
  }

  .third-content {
    border-top: 1rem solid gray;
  }

  .pic-item {
    display: inline-block;
  }

  .fourth-content {
    border-top: 1rem solid gray;
  }

  .info-item{
    border-top: 0.1rem solid lightgrey;
    padding: 0.4rem;
  }
</style>
