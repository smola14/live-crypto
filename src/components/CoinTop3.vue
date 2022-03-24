<template>
  <div class="wrapper">
    <h3><span>Top 3 by price</span></h3>
    <ul>
      <li v-for="coin in coinsByDate" :key="coin.id">
        {{ coin.name }} -
        {{ (Math.round(coin.currentprice * 100) / 100).toFixed(2) }} €
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      coinsByDate: [],
    }
  },
  mounted() {
    axios
      .get(
        `https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&sparkline=false`
      )
      .then((response) => {
        var coins = response.data.map((coin) => this.extractData(coin))
        this.coinsByDate = coins.slice(0)
        this.coinsByDate.sort(function (a, b) {
          return a.currentprice - b.currentprice
        })
        this.coinsByDate.reverse()
        this.coinsByDate.splice(3, coins.length)
      })
  },
  methods: {
    extractData({ name: name, current_price: currentprice }) {
      return { name, currentprice }
    },
  },
}
</script>

<style lang="scss" scoped>
@import '@/style/style.scss';

h3 {
  text-transform: uppercase;
  span {
    border-bottom: 4px solid $color-primary;
  }
}

ul {
  margin-top: em(10);
  padding: 0;
  li {
    list-style-type: none;
    margin: 0;
  }
}
</style>
