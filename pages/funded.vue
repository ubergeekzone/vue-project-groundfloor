<template>
  <b-container>
    <h2 class="title">FUNDED</h2>

    <ul class="funded-list">
      <li v-for="investment in funded" :key="investment.id">
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
    let funded = await $axios.get('http://localhost:3333/api/investment/funded')
    return {
      funded: funded.data
    }
  }
}
</script>
