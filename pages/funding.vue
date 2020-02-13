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
        <p v-if="investment.fundedAmount">
          <span>Funded Amount:</span> ${{ investment.fundedAmount }}
        </p>
        <p v-else>
          <span>Funded Amount:</span> $0
        </p>
      </li>
    </ul>
  </b-container>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    let funding = await $axios.get('/api/funding')
    console.log(funding.data)
    return {
      funding: funding.data
    }
  }
}
</script>

<style>
.funding-list {
  list-style: none;
  margin: 2em 0;
  padding: 0;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-wrap: wrap;
  border-top: 1px solid #ddd7d7;
  border-left: 1px solid #ddd7d7;
  border-bottom: 1px solid #ddd7d7;
  border-right: 1px solid #ddd7d7;
  background-color: #f7f7f7;
}
.funding-list li p:nth-child(1) {
  background-color: #40a6cc;
  padding: 0.2em 1em 0.2em 1em;
  margin-bottom: 0.2em;
}
.funding-list li {
  background-color: #f7f7f7;
  display: flex;
  flex-direction: column;
  width: 50%;
  border-right: 1px solid #ddd7d7;
  border-bottom: 1px solid #ddd7d7;
  padding-bottom: 0.4em;
}

.funding-list li p {
  margin: 0 0 0 0;
}
.funding-list li p a {
  font-weight: bold;
  padding-bottom: 1em;
  color: #fff;
}

.funding-list li p:nth-child(n + 2) {
  display: inline-block;
  padding: 0 1em 0 1em;
}
.funding-list li p:nth-child(n + 2) span {
  font-weight: bold;
}

@media (max-width: 960px) {
  .funding-list {
    display: block;
  }
  .funding-list li {
    width: 100%;
  }
}
</style>
