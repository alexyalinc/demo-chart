<template>
  <div class="block">
    <div class="title">
      Введите сумму, чтобы увидеть прогноз по подписчикам и просмотрам
    </div>
    <div class="input-container">
      <img src="../assets/price.svg" />
      <PriceInput v-model="price" />
      руб.
    </div>
  </div>
</template>

<script>
import PriceInput from "./PriceInput"
export default {
  name: 'Price',
  props: {
    value: {
      type: Number
    }
  },
  components: {
    PriceInput
  },
  data () {
    return {
      price: 10000
    }
  },
  watch: {
    price: function (price) {
      this.$emit("input", price)
    }
  }
}
</script>

<style scoped>
.title {
  font-style: normal;
  font-weight: normal;
  font-size: 2rem;
  line-height: 2.4rem;
  color: var(--black-main);
  margin-bottom: 4rem;
}
.block {
  background: var(--grey-minor);
  border-radius: .6rem;
  padding: 3rem 5rem 5rem 5rem;
}
.input-container {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  font-family: Montserrat;
  font-style: normal;
  font-weight: 500;
  font-size: 1.6rem;
  line-height: 2.6rem;
}
.input-price {
  padding: .8rem 2rem 1rem 2rem;
  margin: 0 2rem;
  background: var(--white-main);
  border: .1rem solid var(--grey-minor);
  box-sizing: border-box;
  border-radius: .6rem;
  font-family: Montserrat;
  font-style: normal;
  font-weight: 500;
  font-size: 1.6rem;
  line-height: 2.6rem;
}
@media only screen and (max-width: 1250px) {
  .input-container {
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  .input-container > * {
    margin-bottom: 2rem;
  }
  .block {
    padding: 2rem 2rem 2rem 2rem;
  }
  .title {
    text-align: center;
  }
}
</style>
