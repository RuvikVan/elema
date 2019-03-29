<template>
  <article>
    <div class="header">
      <div class="header-left">
        <h1 class="score">{{seller.score}}</h1>
        <div class="title">综合评分</div>
        <div class="rank">高于周边商家{{seller.rankRate}}%</div>
      </div>
      <div class="header-right"></div>
    </div>
  </article>
</template>

<script>
export default {
  name: 'ratings',
  props: {
    seller: {
      type: Object
    }
  }
}
</script>

<style scoped>
  .header {
    width: 100%;
    display: flex;
  }

  .header .header-left {
    width: 30%;
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
</style>
