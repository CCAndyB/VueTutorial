<template>
  <div class="hello">
    <h1>{{ info }}</h1>
  </div>
</template>
<script>
const axios = require('axios');

var getFullURL = function(url, options){
    const params = [];
    for (let key in options) {
        params.push(`${key}=${options[key]}`);
    }
    return url + '?' + params.join("&");
}

var apiKey = "YourAPIKey";

var baseUrl = "https://min-api.cryptocompare.com/data/price"

var options = {
    fsym: "BTC",
    tsyms: "USD"
};

var fullURL = getFullURL(baseUrl, options);


export default {
  name: 'HelloWorld',
  data: function() {
		return {
			info: ""
		};
	},
   mounted () {
    axios.get(fullURL, {headers: headers})
      .then(response => (this.info = response))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>