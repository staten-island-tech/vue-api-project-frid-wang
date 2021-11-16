<template>
  <div class="main-container">
    <main class="exchange">
      <section class="currency-requested">
        <input type="text" placeholder="Enter currency type" class="header" v-model="currency"/>
        <!-- <div class="currency-selector">
          <h1 class="selector">Select Currency</h1>
          <ul>
            <li class="name" v-for="name in names" :key="name">{{ name }}</li>
         </ul>
        </div> -->
        
        <input type="text" placeholder="Enter Amount" class="output" v-model="amount"/>
        <button @click="onSubmit">Submit</button>
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
      names:[],
      currency:null,
      amount:null
    
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
        this.result =  Object.values(data.conversion_rates) ;
        console.log(this.result);
        this.names = Object.keys(data.conversion_rates) 
        console.log(this.names)
        console.log(this.names[54])
        console.log(this.result[54])
 
      } catch (error) {
        console.log(error);
      }
    },
  },
  onSubmit(){
    let currency = this.currency;
    let amount = this.amount;
    console.log(currency, amount)
  }
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

/* .currency-selector{
  position: relative;
}
.selector{
  cursor: pointer;
} */


/* ul {
  list-style: none;
  cursor: pointer;
  position: absolute;
  top: 150vh;
  max-width: 15rem; 
  max-height: 15rem; 
  overflow-y: scroll; 
  display: flex;
  flex-direction: column;
  justify-content: space-around;
} */
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
