Official documentation [here](https://min-api.cryptocompare.com/documentation).

## Generate an API key
[Read this guide to generate an API key](https://www.cryptocompare.com/coins/guides/how-to-use-our-api/).

### Using the Cryptocompare API with Vue

## Use the Vue CLI to create a vue project with default setup.
https://cli.vuejs.org/guide/

After installing vue:

vue create hello-world

## Modify the generated vue component src/components/Helloworld.vue in script tag to with your API Key instead
## In order to avoid CORS errors you have to add a online proxy before the address like: https://cors-anywhere.herokuapp.com/ when using headers
```
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

var baseUrl = "https://cors-anywhere.herokuapp.com/https://min-api.cryptocompare.com/data/price"

var options = {
    fsym: "BTC",
    tsyms: "USD"
};

var headers = {
   authorization :"Apikey " + apiKey
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
```
## Change the value in h1 in the template tag to info
```
<template>
  <div class="hello">
    <h1>{{ info }}</h1>
  </div>
</template>
```
## Finally Modify src/App.vue to remove the prop being input and any other additional tags.
```
<template>
  <div id="app">
    <HelloWorld/>
  </div>
</template>
```
## If you dont want to use headers, you can simply call axios with the full url
```
i.e replace
axios.get(fullURL, {headers: headers}) with
axios.get("https://min-api.cryptocompare.com/data/price?fsym=BTC&tsyms=USD&api_key=YourAPIKey")
```
## Type npm run serve into the terminal, then click the link in terminal to open localhost:8080 in a browser.
```
The response from the cryptocompare api should be displayed.

A more complicated example vue project is in the github repository.

Copy the CCAPIEXample.vue and table.vue files from the repository into your components directory.

Modify App.vue to import CCAPIExample.vue instead of HelloWorld.vue and then do npm run serve to view the output.
```