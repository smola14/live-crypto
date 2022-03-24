<template>
  <div class="hero">
    <div class="container">
      <div class="row">
        <div class="col-6 col-lg-4 order-2 order-lg-1 top3">
          <CoinTop3 />
        </div>
        <div class="col-12 col-lg-4 order-1 order-lg-2 title">
          <h1><span>Live</span><span>Crypto</span></h1>
          <h2>Cryptocurrencies in one place</h2>
        </div>
        <div class="col-6 col-lg-4 order-2 order-lg-3 top3">
          <CoinTop3Market />
        </div>
      </div>
    </div>
  </div>
  <svg
    data-name="Layer 1"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 1200 120"
    preserveAspectRatio="none"
  >
    <path
      d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V0H0V27.35A600.21,600.21,0,0,0,321.39,56.44Z"
      class="shape-fill"
      fill="#1D1D1D"
    ></path>
  </svg>
  <CoinSearchForm
    class="mb-5 coin-search-form"
    @add-new-coin="coins = $event"
    @searching="searching = $event"
  />
  <CryptoList :new-coins="coins" :is-searching="searching" />
</template>

<script>
import CoinSearchForm from '@/components/CoinSearchForm.vue'
import CryptoList from '@/components/CryptoList.vue'
import CoinTop3 from '@/components/CoinTop3.vue'
import CoinTop3Market from '@/components/CoinTop3Market.vue'

export default {
  components: {
    CoinSearchForm,
    CryptoList,
    CoinTop3,
    CoinTop3Market,
  },
  data() {
    return {
      coins: [],
      searching: Boolean,
    }
  },
}
</script>
<style lang="scss" scoped>
@import '@/style/style.scss';
.hero {
  padding: em(60);
  background-color: lighten($color-background, 3%);
}

h1 {
  font-size: em(60);
  span:nth-child(1) {
    color: white;
    border-bottom: 4px solid $color-primary;
  }
  span:nth-child(2) {
    color: $color-primary;
    border-bottom: 4px solid white;
  }
}

h2 {
  font-size: em(17);
  margin-top: em(10);
}

li {
  list-style-type: none;
}

img {
  position: absolute;
  left: 0;
  width: 7%;
  opacity: 0.3;
}

svg {
  filter: drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));
}

p {
  background-color: lighten($color-background, 3%);
  text-transform: uppercase;
}

@media (max-width: 991.98px) {
  .title {
    margin-bottom: em(20);
  }

  .top3 {
    line-height: em(27);
  }
}
</style>
