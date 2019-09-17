<template>
  <div>
    {{info}}
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

  }
}
</script>