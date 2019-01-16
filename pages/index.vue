<template>
  <b-container>
    <b-jumbotron>
      <h1 class="title">
        <logo/>
      </h1>
      <h3 class="subtitle">
        Sample interview project for GROUNDFLOOR
      </h3>

      <b-container class="invest-action-buttons">
        <b-row>
          <b-col>
            <b-button size="lg" variant="success">
              FUND A LOAN
            </b-button>
            <b-button size="lg" variant="primary">
              BORROW
            </b-button>
          </b-col>
        </b-row>
      </b-container>        
    </b-jumbotron>
  </b-container>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  async asyncData({ $axios }) {
    let funding = await $axios.get(
      'http://localhost:3333/api/investment/funding'
    )
    let funded = await $axios.get('http://localhost:3333/api/investment/funded')
    return {
      funding: funding.data,
      funded: funded.data
    }
  },
  components: {
    Logo
  },
  data() {
    return {
      key: 'value'
    }
  }
}
</script>

<style>
.invest-action-buttons {
  margin-top: 4em;
}
</style>
