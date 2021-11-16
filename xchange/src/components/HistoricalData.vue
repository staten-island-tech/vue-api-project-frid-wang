<template>
  <div class="main-container">
    <div class="exchange">
      <section class="request">
        <input
          class="currency-input"
          v-model="currency"
          type="text"
          placeholder="Enter Currency"
        />
        <input
          class="amount-input"
          v-model="amount"
          type="text"
          placeholder="Enter Amount"
        />
        <button class="request-submit" v-on:click="submitTest">submit</button>
      </section>
      <section class="response"></section>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currency: null,
      amount: null,
    };
  },
  methods: {
    submitTest() {
      let currency = this.currency;
      let amount = this.amount;
      console.log(currency);
      console.log(amount);
      this.currency = null;
      this.amount = null;
    },
  },
};
</script>

<style scoped>
.main-container {
  width: 100vw;
  height: 80vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.exchange {
  display: flex;
  width: 65vw;
  height: 50vh;
  box-shadow: 25px 20px 2.5rem #3f3f3f;
  border-bottom-left-radius: 12.5vh;
  border-top-right-radius: 12.5vh;
  margin: 2.5vh;
}

.request {
  height: 50vh;
  width: 32.5vw;
  border-bottom-left-radius: 12.5vh;
  background-color: #cfcfcf;
  border-right: 1.5px solid #3f3f3f;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}

.response {
  height: 50vh;
  width: 32.5vw;
  border-top-right-radius: 12.5vh;
  background-color: #cfcfcf;
  border-left: 1.5px solid #3f3f3f;
}

.currency-input {
  width: 15vw;
  height: 1.5rem;
  border-radius: 10px;
  border: none;
}

.amount-input {
  width: 15vw;
  height: 1.5rem;
  border-radius: 10px;
  border: none;
}
</style>
