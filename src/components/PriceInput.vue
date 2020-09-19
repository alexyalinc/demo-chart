<template>
  <input class="input-price" v-model="localValue"/>
</template>

<script>
export default {
  name: 'PriceInput',
  props: {
    value: {
      type: Number
    }
  },
  data () {
    return {
      localValue: null,
      unwatchLocalValue: () => {}
    }
  },
  created() {
    this.formatValue(this.value)
  },
  methods: {
    watchLocalValue() {
      this.unwatchLocalValue = this.$watch('localValue', this.formatValue)
    },
    formatValue(val) {
      this.unwatchLocalValue()
      let str = 0
      if (isNaN(val)) {
        str = val.replaceAll(" ", "")
      } else {
        str = Number(val).toString()
      }
      const lastIndex = str.length-1
      // Если не число, то не даем его написать
      if (isNaN(str[lastIndex])) {
       str = str.substring(lastIndex,0)
      }
      // Добавляем пробелы через каждые 3 числа
      str = str.replace(/\B(?=(\d{3})+(?!\d))/g, " ")
      this.$emit("input", Number(str.replaceAll(" ", "")))
      this.localValue = str
      this.watchLocalValue()
    }
  }
}
</script>

<style scoped>
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
/* Chrome, Safari, Edge, Opera */
.input-price::-webkit-outer-spin-button,
.input-price::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
.input-price[type=number] {
  -moz-appearance: textfield;
}
</style>
