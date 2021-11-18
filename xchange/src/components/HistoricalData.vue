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
        <datepicker
          :format="customFormatter"
          v-model="date"
          placeholder="Select a date"
        />
        <button class="request-submit" v-on:click="fetchHistoricalData">
          submit
        </button>
      </section>
      <section class="response">
        <ul class="response-info">
          <li
            v-for="conversion_amount in conversion_amounts"
            :key="conversion_amount"
          >
            {{ conversion_amount }}
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
import datepicker from "vuejs-datepicker";
var moment = require("moment");

export default {
  components: {
    datepicker,
  },
  data() {
    return {
      currency: null,
      amount: null,
      date: null,
      conversion_amounts: [],
    };
  },
  methods: {
    fetchHistoricalData: async function () {
      try {
        const response = await fetch(
          "https://v6.exchangerate-api.com/v6/31a7b6235f39f82f83fd8af6/history/" +
            this.currency +
            "/" +
            moment(this.date).format("YYYY/MM/DD") +
            "/" +
            this.amount
        );
        const data = await response.json();
        console.log(data);
        let names = Object.keys(data.conversion_amounts);
        let totals = Object.values(data.conversion_amounts);
        let display = names;
        let i = 0;
        let m = 23;
        while (i < 23) {
          display.splice(m, 0, totals[i]);
          m++;
          i++;
        }
        this.conversion_amounts = display;
        this.currency = null;
        this.amount = null;
        this.date = null;
      } catch (error) {
        console.log(error);
      }
    },
    customFormatter(day) {
      return moment(day).format("ddd, MMM Do YYYY");
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

.response-info {
  columns: 2;
  list-style: none;
  font-size: 0.75rem;
}
</style>
