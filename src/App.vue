<template>
  <div>
    <h1>Crypto</h1>
  </div>
  <Input
    :changeAmount="changeAmount"
    :convert="convert"
    :favourite="favourite"
  />
  <p v-if="error != ''">{{ error }}</p>
  <p v-if="result != 0" className="result">{{ result }}</p>
  <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs" />
  <div class="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
  </div>
</template>

<script>
import Input from "./components/Input.vue";
import Selector from "./components/Selector.vue";
import CryptoConvert from "crypto-convert";
import Favourite from "./components/Favourite.vue";

const convert = new CryptoConvert();

export default {
  components: { Input, Selector, Favourite },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: [],
    };
  },

  methods: {
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
    },
    favourite() {
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond,
      });
    },
    changeAmount(val) {
      this.amount = val;
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },
    async convert() {
      if (this.cryptoFirst == "" || this.cryptoSecond == "") {
        this.error = "Choose the currency for converting";
        return;
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = "Similar currencies can't be converted";
        return;
      } else if (this.amount <= 0) {
        this.error = "Amount should be more than 0";
        return;
      }
      this.error = "";

      await convert.ready();

      if (this.cryptoFirst == "BTC" && this.cryptoSecond == "ETH")
        this.result = convert.BTC.ETH(this.amount);
      else if (this.cryptoFirst == "BTC" && this.cryptoSecond == "USDT") {
        this.result = convert.BTC.USDT(this.amount);
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "BTC") {
        this.result = convert.ETH.BTC(this.amount);
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "USDT") {
        this.result = convert.ETH.USDT(this.amount);
      } else if (this.cryptoFirst == "USDT" && this.cryptoSecond == "BTC") {
        this.result = convert.USDT.BTC(this.amount);
      } else if (this.cryptoFirst == "USDT" && this.cryptoSecond == "ETH") {
        this.result = convert.USDT.ETH(this.amount);
      }
    },
  },
};
</script>

<style>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 500px;
  margin: 0 auto;
  gap: 100px;
}
.result {
  font-family: "Bungee Spice", sans-serif;
  font-size: 30px;
}
</style>
./components/Selector.vue./components/Input.vue./components/Favourite.vue
