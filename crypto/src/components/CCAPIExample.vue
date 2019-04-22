<template>
  <div class="flexbox">
    <div>
<!--      <h1>{{ USD }}</h1>-->

      <table>
        <tr>
          <th>Image</th>
          <th>Full Name</th>
          <th>Name</th>
          <th>PRICE</th>
          <th>SUPPLY</th>
        </tr>
        <tr v-for="(coin, index) in all_coins" :key="index">
          <td><img :src="'https://www.cryptocompare.com' + coin.CoinInfo.ImageUrl + '?width=30'" alt=""></td>
          <td>{{coin.CoinInfo.FullName}}</td>
          <td>{{coin.CoinInfo.Name}}</td>
          <td>{{coin.RAW.USD.PRICE}}</td>
          <td>{{coin.RAW.USD.SUPPLY}}</td>
        </tr>
      </table>

    </div>
  </div>
</template>

<script>
const axios = require("axios");
export default {
  name: "Crypto",
  data: function() {
    return {
      crypto: [],
      all_coins: []
    };
  },
  async created() {
    this.getData()
     await setInterval(() => this.getData(), 300000)
  },
  methods: {
    sort(a, b) {
      return b.RAW.USD.PRICE - a.RAW.USD.PRICE
    },
    async getData() {
      this.all_coins = []
      await axios.get("https://min-api.cryptocompare.com/data/top/mktcapfull?limit=20&tsym=USD").then(
        response => (this.crypto = response.data.Data));
      if(this.crypto.length > 0) {
        this.crypto.forEach(item => {
          this.all_coins.push(item);
          return this.all_coins
        });
      }

      this.all_coins = this.all_coins.sort(this.sort);


    }
  }
};
</script>

<style scoped l>
  td, th {
    border: 1px solid black;
  }
</style>
