<template>
  <div>
    <!-- {{info}} -->

    <div 
      v-for="currency in info"
      v-bind:key="currency.code"
      >
      {{currency.description}}

      <span class="lighten">
        <span v-html="currency.symbol"></span>{{ currency.rate_float | currencydecimal }}
      </span>
    </div>

    


  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      info: null
    }
  },

  created() {
    axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(response => (this.info = response.data.bpi))
      .catch(e => {
      this.errors.push(e)
    })
  },
  filters: {
    currencydecimal ( value ) {
      return value.toFixed(2)
    }
  }
}
</script>