/* eslint-disable */
<template>
  <h2 v-if="newCoins.length == 0">No currency found.</h2>

  <table v-else>
    <thead>
      <tr>
        <th>#</th>
        <th>Name</th>
        <th>Price</th>
        <th>Change in 24</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="coin in newCoins" :key="coin.id">
        <td><img class="coin-image" :src="coin.img" :alt="coin.name" /></td>
        <td>{{ coin.name }}</td>
        <td>{{ (Math.round(coin.currentprice * 100) / 100).toFixed(2) }} €</td>
        <td :style="coinColor(coin.change24)">
          {{ (Math.round(coin.change24 * 100) / 100).toFixed(2) }} €
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    'is-searching': {
      default: false,
      type: Boolean,
    },
    'new-coins': {},
  },
  data() {
    return {}
  },
  methods: {
    coinColor(data) {
      if (data > 0) {
        return 'color:lightgreen'
      } else {
        return 'color:red'
      }
    },
  },
}
</script>

<style lang="scss" scoped>
@import '@/style/style.scss';

table {
  margin: 0 auto;
  border-spacing: 2em 1em;
  text-align: left;
}

td,
th {
  border: 1px solid #999;

  padding: em(10);
}

.coin-image {
  height: em(30);
  width: em(30);
}
</style>
