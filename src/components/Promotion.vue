<template>
  <div>
    <div class="title">Прогноз продвижения</div>
    <div class="container">
      <div class="block">
        <div class="description">
          Мы пользуемся только официальными инструментами рекламы, рекомендуемыми самим YouTube, поэтому все приведенные нами просмотры, лайки и комментарии будут настоящими, а подписчики живыми и заинтересованными в тематике Вашего канала
        </div>
        <Price v-model="price" />
        <div class="help">
          Прогноз подписчиков зависит от Вашего контента. Сделайте его интересным и старайтесь не снижайть планку
        </div>
      </div>
      <div class="block">
        <Chart :price="price" />
      </div>
    </div>
  </div>
</template>

<script>
import Price from "./Price"
import Chart from "./Chart"
export default {
  name: 'Promotion',
  components: {
    Price,
    Chart
  },
  data () {
    return {
      price: 10000
    }
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  display: flex;
}
.container > .block {
  padding:0 7.6rem 0 7.6rem;
  flex: 1 1 50rem;
  width: 50%;
}
.title {
  font-style: normal;
  font-weight: bold;
  font-size: 4.6rem;
  line-height: 6.4rem;
  text-align: center;
  padding:10rem 7.6rem 6rem 7.6rem;
  width: 100%;
}
.description {
  font-style: normal;
  font-weight: 500;
  font-size: 1.6rem;
  line-height: 2.6rem;
  color: var(--grey-body-landing);
  margin-bottom: 4.8rem;
}
.help {
  font-family: Montserrat;
  font-style: normal;
  font-weight: normal;
  font-size: 1.5rem;
  line-height: 2.2rem;
  letter-spacing: 0.02em;
  color: var(--black-minor);
  margin-top: 3rem;
}
@media only screen and (max-width: 1250px) {
  .container {
    flex-wrap: wrap;
    flex-direction: column;
  }
  .container > .block {
    padding:0 1.6rem 0 1.6rem;
    width: 100%;
  }
  .title {
    padding:4rem 0rem 3rem 0rem;
  }
  .description {
    text-align: center;
  }
  .help {
    text-align: center;
  }
}
</style>
