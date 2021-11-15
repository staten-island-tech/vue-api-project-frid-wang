<template>
  <div class="main-container">
    <main class="exchange">
      <section class="currency-requested">
        <!-- <input type="text" placeholder="Enter currency type" class="header"/> -->
        <div class="currency-selector">
          <ul>
            <li v-for="rate in arr" :key="rate">{{ rate }}</li>
          </ul>
        </div>
        <input type="text" placeholder="Enter Amount" class="output" />
      </section>
      <section class="currency-returned">
        <input type="text" class="header" placeholder="Enter currency type" />
        <div class="output"></div>
      </section>
    </main>
    <main class="reset">
      <button class="reset-button">Reset</button>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      result: [],
      arr: [],
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData: async function () {
      try {
        const response = await fetch(
          "https://v6.exchangerate-api.com/v6/31a7b6235f39f82f83fd8af6/latest/USD"
        );
        const data = await response.json();
        console.log(data);
        console.log(data.conversion_rates);
        this.result = data.conversion_rates;
        console.log(this.result);
        Object.keys(this.result).forEach((key) => {
          this.arr.push({ [key]: this.result[key] });
        });
        console.log(this.arr);
      } catch (error) {
        console.log(error);
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
  width: 55vw;
  height: 50vh;
  box-shadow: 25px 20px 2.5rem #3f3f3f;
  border-bottom-left-radius: 12.5vh;
  border-top-right-radius: 12.5vh;
  margin: 2.5vh;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.currency-requested {
  display: flex;
  flex-direction: column;
  height: 70%;
  justify-content: space-around;
}

.currency-returned {
  display: flex;
  flex-direction: column;
  height: 70%;
  justify-content: space-around;
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
  cursor: pointer;
}

.output {
  height: 3rem;
  border: solid;
}

.output:focus {
  outline: none;
}

.header:focus {
  outline: none;
}
</style>
