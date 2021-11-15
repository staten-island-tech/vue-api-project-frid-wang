<template>
  <div class="main-container">
    <div class="exchange">
      <section class="request">
        <form>
          <input v-model="currency" type="text" />
          <input v-model="amount" type="text" />
          <button v-on:click="submitTest" type="submit" />
        </form>
      </section>
      <section class="response"></section>
    </div>
    <div class="reset">
      <button class="reset-button">Reset</button>
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
      if (this.currency && this.amount) {
        let currency2 = this.currency;
        let amount2 = this.amount;
        this.currency = null;
        this.amount = null;
        console.log(currency2);
        console.log(amount2);
      } else {
        console.log("error");
      }
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

.reset {
  width: 10vw;
  height: 5vh;
}

.reset-button {
  width: 10vw;
  height: 5vh;
  box-shadow: 2.5px 2px 0.25rem #3f3f3f;
  border-top-left-radius: 2.5vh;
  border-bottom-right-radius: 2.5vh;
  margin: 2.5vh;
  border: none;
  font-size: 1.25rem;
}

.request {
  height: 50vh;
  width: 32.5vw;
  background-color: aqua;
  border-bottom-left-radius: 12.5vh;
}
.response {
  height: 50vh;
  width: 32.5vw;
  background-color: red;
  border-top-right-radius: 12.5vh;
}
</style>
