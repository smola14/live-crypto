<template>
  <li class="crypto-list-coin">{{ coin.name }} | {{ coin.currentprice }}€</li>
</template>

<script>
export default {
  props: {
    coin: {
      type: Object,
    },
  },
}
</script>

<style lang="scss" scoped>
li {
  list-style-type: none;
}
</style>
