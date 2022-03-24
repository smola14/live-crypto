/* eslint-disable */
<template>
  <div class="wrapper">
    <h3><span>Top 3 by % change in 24H</span></h3>
    <ul>
      <li v-for="coin in coinsByChange24" :key="coin.id">
        {{ coin.name }} -
        {{ (Math.round(coin.change24 * 100) / 100).toFixed(2) }} %
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      coinsByChange24: [],
    }
  },
  mounted() {
    axios
      .get(
        `https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&sparkline=false`
      )
      .then((response) => {
        var coins = response.data.map((coin) => this.extractData(coin))
        this.coinsByChange24 = coins.slice(0)
        this.coinsByChange24.sort(function (a, b) {
          return a.change24 - b.change24
        })
        this.coinsByChange24.reverse()
        this.coinsByChange24.splice(3, coins.length)
      })
  },
  methods: {
    extractData({ name: name, price_change_percentage_24h: change24 }) {
      return { name, change24 }
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
