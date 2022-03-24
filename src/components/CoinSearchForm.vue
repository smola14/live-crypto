/* eslint-disable */
<template>
  <form>
    <search-icon size="1.5x" class="icon search-icon" />
    <input
      @keyup="getCoins()"
      v-model="query"
      type="text"
      ref="input"
      class="form-control"
    />
    <rotate-cw-icon
      @click.prevent="getCoins()"
      size="1.5x"
      class="icon reload-icon"
    />
  </form>
</template>

<script>
import axios from 'axios'

import { RotateCwIcon, SearchIcon } from '@zhuowenli/vue-feather-icons'

export default {
  components: {
    SearchIcon,
    RotateCwIcon,
  },
  data() {
    return {
      query: '',
      coins: [],
    }
  },
  methods: {
    getCoins() {
      axios
        .get(
          `https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&sparkline=false`
        )
        .then((response) => {
          if (this.query == '') {
            this.coins = response.data.map((coin) => this.extractData(coin))
            this.$emit('add-new-coin', this.coins)
          } else {
            this.coins = response.data
              .filter((coin) => coin.name.toLowerCase().includes(this.query))
              .map((coin) => this.extractData(coin))
            this.$emit('add-new-coin', this.coins)
          }
        })
    },
    extractData({
      name: name,
      current_price: currentprice,
      image: img,
      price_change_24h: change24,
    }) {
      return { name, currentprice, img, change24 }
    },
  },
  created() {
    this.getCoins()
  },
}
</script>

<style lang="scss" scoped>
@import '@/style/style.scss';
form {
  width: 25%;
  display: flex;
  margin-left: auto;
  margin-right: auto;

  input {
    margin: 0 em(5);
    color: white !important;
    width: 100%;
    text-align: center;
    border-radius: 4px;
    border: 2px solid white;
    background: lighten($color-background, 5%);
    box-shadow: none !important;
    border: 2px solid $color-primary;
    &:active,
    &:focus {
      background-color: lighten($color-background, 5%);
      border: 2px solid $color-primary;
    }
  }
}

.icon {
  font-size: em(20);
  margin-top: em(2);
}

.reload-icon {
  cursor: pointer;
}
</style>
