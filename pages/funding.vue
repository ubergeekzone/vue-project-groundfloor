<template>
  <b-container>
    <h2 class="title">FUNDING</h2>

    <ul class="funding-list">
      <li v-for="investment in funding" :key="investment.id">
        <p>
          <nuxt-link :to="'/investment/' + investment.id">
            {{ investment.address }}
          </nuxt-link>
        </p>
        <p>
          <span>Your Loan Amount:</span> ${{ investment.loan_amount_dollars }}
        </p>
        <p>
          <span>Loan Purpose:</span> {{ investment.purpose }}
        </p>
        <p>
          <span>Expected Term Purpose: </span> {{ investment.expected_term_months }}
        </p>
        <p>
          <span>Rate:</span> {{ investment.rate }}%
        </p>
      </li>
    </ul>
  </b-container>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    let funding = await $axios.get('/api/funding')
    return {
      funding: funding.data
    }
  }
}
</script>

<style>
ul {
  list-style: none;
  margin: 2em 0;
  padding: 0;
}
p {
  margin: 0.2em 0 0.2em 0;
}
p a {
  font-weight: bold;
}

p:nth-child(n + 2) {
  display: block;
  padding: 0 2em 2em 0;
  float: left;
}
p:nth-child(n + 2) span {
  font-weight: bold;
}

@media (max-width: 960px) {
  p:nth-child(n + 2) {
    display: block;
    padding: 0 0.2em 0.2em 0;
    float: inherit;
  }
}
</style>
