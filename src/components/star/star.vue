<template>
  <div class="star" :class="starType">
    <span v-for="itemClass in itemClasses" :class="itemClass" class="star-item" :key="itemClass"></span>
  </div>
</template>

<script>

const LENGTH = 5
const CLS_ON = 'on'
const CLS_HALF = 'half'
const CLS_OFF = 'off'

export default {
  name: 'star',
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  computed: {
    starType () {
      return 'star-' + this.size
    },
    itemClasses () {
      let result = []
      let score = Math.floor(this.score * 2) / 2
      let hasDecimal = score % 1 !== 0
      let integer = Math.floor(score)
      for (let i = 0; i < integer; i++) {
        result.push(CLS_ON)
      }
      if (hasDecimal) {
        result.push(CLS_HALF)
      }
      while (result.length < LENGTH) {
        result.push(CLS_OFF)
      }
      return result
    }
  }
}
</script>

<style scoped>

  .star-24 .on {
    background: url("../../assets/star/star24_on@2x.png");
    width: 0.5rem;
    height: 0.5rem;
    background-repeat: no-repeat
  }

  .star-24 .half {
    background: url("../../assets/star/star24_half@2x.png");
    width: 0.5rem;
    height: 0.5rem;
    background-repeat: no-repeat
  }

  .star-24 .off {
    background: url("../../assets/star/star24_off@2x.png");
    width: 0.5rem;
    height: 0.5rem;
    background-repeat: no-repeat
  }

  .star-item {
    display: inline-block;
  }
</style>
