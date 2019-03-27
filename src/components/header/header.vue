<template>
  <header>
    <div class="header-content-top">
      <img src="http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg">
      <div class="header-content-top-text">
        <div class="header-content-top-image">
          <img src="../../assets/header/brand@2x.png">
          <p>
            {{ seller.name }}
          </p>
        </div>
        <div class="header-content-top-description">
          <p>{{ seller.description }} / {{ seller.deliveryTime }}分钟送到</p>
        </div>
        <div class="header-content-top-support">
          <img src="../../assets/header/decrease_1@2x.png">
          <p v-if="seller.supports">
            {{ seller.supports[0].description }}
          </p>
        </div>
      </div>
    </div>
    <div class="header-content-bottom">
      <img src="../../assets/header/bulletin@2x.png">
      <p>
        {{ seller.bulletin }}
      </p>
    </div>
  </header>
</template>

<script>
export default {
  name: 'header',
  props: {
    seller: {
      type: Object
    }
  }
}
</script>

<style scoped>
  header {
    height: 4rem;
    display: flex;
    flex-direction: column;
    background: rgba(7, 17, 27, 0.5)
  }

  .header-content-top {
    display: flex;
    flex-direction: row;
    width: 100%;
  }

  .header-content-top > img {
    width: 2rem;
    height: 2rem;
    margin-top: 0.75rem;
    margin-left: 0.5rem;
  }

  .header-content-top-text {
    display: flex;
    flex-direction: column;
    margin-top: 0.5rem;
    margin-left: 0.5rem;
    height: 2rem;
  }

  .header-content-top-text p {
    color: white;
    font-size: 0.4rem;
  }

  .header-content-top-image {
    display: flex;
    flex-direction: row;
    margin-top: 0.25rem;
  }

  .header-content-top-image > img {
    width: 0.8rem;
    height: 0.5rem;
  }

  .header-content-top-image > p {
    margin-left: 0.5rem;
  }

  .header-content-top-description {
    margin-top: 0.3rem;
  }

  .header-content-top-support {
    display: flex;
    flex-direction: row;
    margin-top: 0.25rem;
  }

  .header-content-top-support > img {
    width: 0.55rem;
    height: 0.5rem;
  }

  .header-content-top-support > p {
    margin-left: 0.5rem;
  }

  .header-content-bottom {
    width: 100%;
    height: 0.8rem;
    display: flex;
    flex-direction: row;
    margin-top: 0.5rem;
    background: rgba(0, 0, 0, 0.2);
  }

  .header-content-bottom p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    color: white;
    margin-top: 0.1rem;
    margin-left: 0.1rem;
  }

  .header-content-bottom img {
    width: 0.5rem;
    height: 0.3rem;
    margin-top: 0.1rem;
    margin-left: 0.2rem;
  }
</style>
