<template>
  <div class="flexbox">
    <div>
      <h1>Vue CryptoCompare Api Guide</h1>
    </div>
    <div class="padding">
      <table class="style position">
        <tr>
          <th>Type</th>
          <th>MARKET</th>
          <th>FROMSYMBOL</th>
          <th>TOSYMBOL</th>
          <th>image</th>
        </tr>
        <tr>
          <td>{{USD.TYPE}}</td>
          <td>{{USD.MARKET}}</td>
          <td>{{USD.FROMSYMBOL}}</td>
          <td>{{USD.TOSYMBOL}}</td>
          <td>
            <img v-bind:src="USDimg">
          </td>
        </tr>
        <tr>
          <td>{{USD.TYPE}}</td>
          <td>{{USD.MARKET}}</td>
          <td>{{USD.FROMSYMBOL}}</td>
          <td>{{USD.TOSYMBOL}}</td>
          <td>
            <img v-bind:src="USDimg">
          </td>
        </tr>
      </table>
    </div>
    <div>
      <button v-on:click="getData">Get Data</button>
      <div class="padding">
        <tableComponent v-if="ok" v-bind:exchangeInfo="VOLUME" ></tableComponent>
      </div>
    </div>
  </div>
</template>

<script>
const axios = require("axios");
import tableComponent from './table'

var getFullURL = function(url, options) {
  const params = [];
  for (let key in options) {
    params.push(`${key}=${options[key]}`);
  }
  return url + "?" + params.join("&");
};

var apiKey = "";

var baseUrl = "https://cors-anywhere.herokuapp.com/https://min-api.cryptocompare.com/data/pricemultifull";

var options = {
  fsyms: "BTC",
  tsyms: "USD,EUR"
};

var headers = {
  "Authorization": "Apikey " + apiKey 
};

var fullURL = getFullURL(baseUrl, options);

export default {
  name: "HelloWorld",
  components: {tableComponent},
  data: function() {
    return {
      USD: "",
      EUR: "",
      EURimg: "",
      USDimg: "",
      VOLUME: [],
      test:"hello",
      ok: false
    };
  },
  mounted() {
    axios
      .get(fullURL, { headers: headers })
      .then(
        response => (
          (this.USD = response.data.RAW.BTC.USD),
          (this.USDimg =
            "https://www.cryptocompare.com" +
            response.data.RAW.BTC.USD.IMAGEURL +
            "?width=50"),
          (this.EUR = response.data.RAW.BTC.EUR),
          (this.EURimg =
            "https://www.cryptocompare.com" +
            response.data.RAW.BTC.EUR.IMAGEURL +
            "?width=50")
        )
      );
  },
  methods: {
    setOkTrue: function() {
      this.ok = true;
    },
    getData: function() {
      axios.get("https://min-api.cryptocompare.com/data/top/exchanges?fsym=BTC&tsym=USD&api_key=").then(
        response => (this.VOLUME = response.data.Data),
        this.setOkTrue())
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.style {
  background-color: rgb(73, 216, 124);
  color: white;
  border: 1px solid black;
}
.position {
  margin: auto;
}
.flexbox {
  display: flex;
  flex-direction: column;
}

.padding {
  padding: 50px;
}
</style>
