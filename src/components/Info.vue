<template>
  <div class="currency">

    <b-container class="bv-example-row">
      <!-- Image and text -->
      <b-navbar variant="light" type="light">
        <b-navbar-brand href="#">
          <b-img src="https://dorokhin.moscow/static/favicon.png" fluid alt="logo" />
          Курс Bitcoin
        </b-navbar-brand>
      </b-navbar>


    <div id="currency" v-for="(value, key) in currency">
      <span class="left">{{ key }}</span>
      <span class="right">{{ value.last }} {{ value.symbol }}</span>
    </div>

    </b-container>

  </div>
</template>

<style>
  body {
    background: #fff;
  }

  div#currency {
    background: #f9f9f9;
    width: 100%;
    margin: 0 auto 4px auto;
    padding: 1em;
    box-shadow: 1px 1px 0 lightgrey;
  }

  span.left {
    font-weight: bold;
  }

  span.right {
    float:right;
  }
</style>


<script>
  import axios from 'axios'

  export default {
    name: 'info',
    data: () => ({
      currency: [],
      errors: []
    }),

    created () {
      axios.get('https://blockchain.info/ticker')
        .then(response => {
          this.currency = response.data
          console.log(response)         // This will give you access to the full object
        })
        .catch(e => {
          this.errors.push(e)
        })
    }
  }
</script>
