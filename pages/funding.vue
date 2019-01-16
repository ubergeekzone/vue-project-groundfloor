<template>
  <b-container>
    <h2 class="title">FUNDING</h2>

    <ul class="funding-list">
      <li v-for="investment in funding" :key="investment.id">
        <p>
          {{ investment.address }}
        </p>
        <p>
          {{ investment.loan_amount_dollars }}
        </p>
      </li>
    </ul>
  </b-container>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    let funding = await $axios.get(
      'http://localhost:3333/api/investment/funding'
    )
    return {
      funding: funding.data
    }
  }
}
</script>
