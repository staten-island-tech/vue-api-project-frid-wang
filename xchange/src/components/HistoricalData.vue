<template>
  <div class="main-container">
    <div class="date-warn">
      <p>{{ $attrs.warning }}</p>
    </div>
    <div class="exchange">
      <section class="request" v-bind:style="requestStyle">
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
          :disabled-dates="disabledDates"
          :format="customFormatter"
          v-model="date"
          placeholder="Select a date"
        />
        <button class="request-submit" v-on:click="fetchHistoricalData">
          SUBMIT
        </button>
      </section>
      <section class="response" v-bind:style="responseStyle">
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
      disabledDates: {
        to: new Date(2000, 0, 1), // Disable all dates up to specific date
        from: new Date(2021, 10, 31),
      },
      responseStyle: {},
      requestStyle: {},
      scrollStyleRes: {
        maxHeight: "50vh",
        overflowY: "scroll",
        borderTopRightRadius: "0vh",
        borderBottomRightRadius: "0vh",
      },
      scrollStyleReq: {
        borderBottomLeftRadius: "0vh",
        borderTopLeftRadius: "0vh",
      },
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
        let display = [];
        let i = 0;

        while (i < names.length) {
          display.push(String(names[i]) + " " + String(totals[i]));
          i++;
        }
        this.conversion_amounts = display;
        this.responseStyle = this.scrollStyleRes;
        this.requestStyle = this.scrollStyleReq;
        this.currency = null;
        this.amount = null;
        this.date = null;
      } catch (error) {
        alert(
          "There was a problem fulfilling your request, please confirm that all inputs were spelled correctly, and that no fields were left blank. Thank you, and sorry for any inconvenience"
        );
      }
    },
    customFormatter(day) {
      return moment(day).format("ddd, MMM Do YYYY");
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Unica+One&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;500&display=swap");

.main-container {
  width: 100vw;
  height: 80vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Unica;
  font: 600;
}

.exchange {
  display: flex;
  width: 65vw;
  height: 50vh;
  box-shadow: 25px 20px 2.5rem #3f3f3f;
  border-radius: 5vh;
  margin: 2.5vh;
}

.request {
  height: 50vh;
  width: 32.5vw;
  border-bottom-left-radius: 5vh;
  border-top-left-radius: 5vh;
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
  border-top-right-radius: 5vh;
  border-bottom-right-radius: 5vh;
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
  list-style: none;
  font-size: 1rem;
  line-height: 150%;
  max-width: 32.5;
}

.ISO-list {
  columns: 6;
  list-style: none;
}

.iso-title {
  font-size: 1.25rem;
}

.iso-container {
  width: 25vw;
  margin: 5vh;
  display: flex;
  flex-direction: column;
  align-content: center;
}

.date-warn {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  width: 45vw;
  height: 5vh;
  background-color: #d45434;
  filter: brightness(110%);
  border-radius: 2vh;
  font-family: "Open Sans";
  font: 500;
}

.request-submit {
  border: none;
  background-color: #afafaf;
  font-size: 1rem;
  height: 1.75rem;
  width: 7.5vw;
  border-radius: 0.75rem;
}

.request-submit:hover {
  transform: scale(1.1);
  box-shadow: 0px 3px 5px #3f3f3f;
}
</style>
