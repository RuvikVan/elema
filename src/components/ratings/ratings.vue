<template>
  <article>
    <div class="header">
      <div class="header-left">
        <h1 class="score">{{seller.score}}</h1>
        <div class="title">综合评分</div>
        <div class="rank">高于周边商家{{seller.rankRate}}%</div>
      </div>
      <div class="header-right">
        <div class="header-right-top">
          <span class="score-right">商品评分</span>
          <v-star :size="24" :score="seller.foodScore" class="qwe1"></v-star>
        </div>
        <div class="header-right-bottom">
          <span class="title">送达时间</span>
          <span class="delivery">{{seller.deliveryTime}}分钟</span>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="evaluate">
        <div class="all" @click="showAll">全部 {{ allNum }}</div>
        <div class="satisfied" @click="showSatisfied">满意 {{ satisfiedNum }}</div>
        <div class="unsatisfied" @click="showUnsatisfied">不满意 {{ unsatisfiedNum }}</div>
      </div>
      <div class="evaluate-content" ref="evaluateContent">
        <ul>
          <li class="rate" v-for="rate in copyRatings" :key="rate">
<!--            <div content="evaluate-content-li">-->
<!--              <div class="evaluate-content-li-left">-->
<!--                <img width="28" height="28" :src="rate.avatar">-->
<!--              </div>-->
<!--              <div class="evaluate-content-li-right"></div>-->
<!--            </div>-->
            <span>{{rate.text}}</span>
          </li>
        </ul>
      </div>
    </div>
  </article>
</template>

<script>
import star from '../star/star'
import axios from 'axios'
import BScroll from 'better-scroll'

export default {
  name: 'ratings',
  methods: {
    showAll () {
      this.copyRatings = this.ratings
    },
    showSatisfied () {
      this.copyRatings = []
      this.ratings.forEach((item, index) => {
        if (item.rateType === 0) {
          this.copyRatings.push(item)
        }
      })
    },
    showUnsatisfied () {
      this.copyRatings = []
      this.ratings.forEach((item, index) => {
        if (item.rateType === 1) {
          this.copyRatings.push(item)
        }
      })
      console.log(this.copyRatings)
    }
  },
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      ratings: [],
      copyRatings: [],
      allNum: 0,
      satisfiedNum: 0,
      unsatisfiedNum: 0
    }
  },
  components: {
    'v-star': star
  },

  created () {
    axios.get('http://118.25.61.61:8080/data/data.json').then((res) => {
      this.ratings = res.data.ratings
      this.ratings.forEach((item, index) => {
        this.allNum += 1
        if (item.rateType === 0) {
          this.satisfiedNum += 1
        }
        if (item.rateType === 1) {
          this.unsatisfiedNum += 1
        }
      })
      this.copyRatings = this.ratings
    })
    this.$nextTick(() => {
      this.menuScroll = new BScroll(this.$refs.evaluateContent, {})
    })
  }
}
</script>

<style scoped>

  .header {
    width: 100%;
    display: flex;
  }

  .header .header-left {
    width: 40%;
    border-right: 0.02rem solid rgba(7, 17, 27, 0.5);
    text-align: center;
    margin: 0.5rem;
  }

  .header .header-left .score {
    color: orange;
    font-size: 0.8rem;
  }

  .header .header-left .rank {
    color: rgba(7, 17, 27, 0.5);
    font-size: 0.1rem;
  }

  .header-right {
    width: 60%;
    display: flex;
    flex-direction: column;
    margin: 0.5rem;
  }

  .qwe1 {
    display: inline-block;
  }

  .header-right-top {

  }

  .header-right-bottom {
    margin-top: 0.8rem;
  }

  .content {
    border-top: 0.5rem solid lightgrey;
  }

  .evaluate {
    display: flex;
    flex-direction: row;
    margin: 0.5rem 0 0 0.5rem;
  }

  .all {
    width: 2rem;
    height: 1rem;
    background: lightblue;
    line-height: 1rem;
    text-align: center;
  }

  .satisfied {
    width: 2rem;
    height: 1rem;
    background: dodgerblue;
    line-height: 1rem;
    text-align: center;
    margin-left: 0.5rem;
  }

  .unsatisfied {
    width: 2rem;
    height: 1rem;
    background: lightslategrey;
    line-height: 1rem;
    text-align: center;
    margin-left: 0.5rem;
  }

  .evaluate-content {
    margin-top: 0.5rem;
    max-height: 6rem;
    width: 100%;
    overflow: hidden;
  }

  .evaluate-content li {
    /*border-top: 0.1rem solid black;*/
    /*border-bottom: 0.1rem solid black;*/
  }

  .evaluate-content li span {
    font-size: 0.5rem;
  }
</style>
