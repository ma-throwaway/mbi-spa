<template>
  <div style="padding-bottom:20px;">
    <button v-on:click="sendRequest">Get MBI</button>
    <div>{{ generateResponse }}</div>
  </div>

  <div>
    <input v-model="mbi" placeholder="Enter MBI to Verify">
    <button v-on:click="verifyMbi">Submit</button>
    <div> {{ verifyResponse }} </div>
  </div>
</template>

<script>
  const axios = require("axios");

  export default {
    name: 'App',
    data: function () {
      return {
        generateResponse: null,
        verifyResponse: null,
        mbi: ""
      };
    },
    beforeMount() {},
    methods: {
      sendRequest() {
        this.getMBI("https://mbi-api-mga.herokuapp.com/generate");
      },
      async getMBI(url) {
        axios
            .get(url)
            .then(response => {this.generateResponse = response.data.mbi})
      },
      verifyMbi() {
        this.verifyMBI("https://mbi-api-mga.herokuapp.com/verify");
      },
      async verifyMBI(url) {
        axios.post(url, {
          mbi: this.mbi,
        })
        .then(response => {this.verifyResponse = response.data})

      },
    }
  };
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
