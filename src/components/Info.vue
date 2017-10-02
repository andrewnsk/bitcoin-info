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

      <div>
        <table class="table table-hover">
          <thead>
          <tr>
            <th>Валюта</th>
            <th>Покупка</th>
            <th>Продажа</th>
            <th>Последняя</th>
            <th>Символ</th>
          </tr>
          </thead>
          <tfoot>
          <tr>
            <th>Валюта</th>
            <th>Покупка</th>
            <th>Продажа</th>
            <th>Последняя</th>
            <th>Символ</th>
          </tr>
          </tfoot>
          <tbody>
          <tr v-for="(value, key) in currency">
            <td>{{ key }}</td>
            <td>{{ value.buy }}</td>
            <td>{{ value.sell }}</td>
            <td>{{ value.last }}</td>
            <td>{{ value.symbol }}</td>
          </tr>

          </tbody>
        </table>
      </div>
<!--    <div id="currency" v-for="(value, key) in currency">
      <span class="left">{{ key }}</span>
      <span class="right">{{ value.last }} {{ value.symbol }}</span>
    </div>-->

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
      errors: [],

      fields: [
        {
          key: 'symbol',
          sortable: true
        },
        {
          key: 'buy',
          sortable: false
        }
      ],
      data_items: [
      ]
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
