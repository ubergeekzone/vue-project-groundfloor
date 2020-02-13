<template>
  <b-container>
    <h1 class="title">LOAN</h1>
    <p>Address: {{ investment.address }}</p>
    <p>Purpose: {{ investment.purpose }}</p>

    <b-form @submit="onSubmit">

      <b-form-group label="Fund Amount"
                    label-for="amount">
        <b-input-group>
          <b-input-group-prepend>
            <span class="input-group-text">$</span>
          </b-input-group-prepend>
          <b-form-input id="amount"
                        v-model="amount"
                        type="number"
                        name="amount"/>
        </b-input-group>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>

    </b-form>

    <hr>

    <section class="investment_funds">
      <h3 class="subtitle">Loan Funds <small>(${{ fundedTotalAmount }} has been funded for this loan)</small></h3>
      <ul>
        <li v-for="funded in funds" :key="funded.id">
          ${{ funded.amount }}
        </li>
      </ul>
    </section>
    
    <p>
      <b-button type="button" vairant="success" @click="goBack">
        Back
      </b-button>
    </p>

  </b-container>
</template>
<script>
export default {
  async asyncData({ $axios, params }) {
    let investment = await $axios.get(`/api/investment/${params.id}`)
    let funds = await $axios.get(`/api/investment/${params.id}/funds`)
    let fundedTotalAmount = 0
    funds.data.forEach(function(funded) {
      fundedTotalAmount += funded.amount
    })
    return {
      investment: investment.data,
      funds: funds.data,
      amount: investment.data.loan_amount_dollars,
      fundedTotalAmount: fundedTotalAmount,
      investment_id: params.id
    }
  },
  methods: {
    goBack() {
      this.$router.back()
    },
    async onSubmit(ev) {
      ev.preventDefault()
      let { investment_id, amount } = this
      let b = {
        investment_id,
        amount
      }
      let investments = await this.$axios({
        method: 'post',
        url: '/api/funding',
        data: b
      })
    }
  }
}
</script>
