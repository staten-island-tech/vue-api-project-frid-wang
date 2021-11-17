<template>
  <div class="main-container">
    <main class="exchange">
      <section class="currency-requested">

        <div class="currency-selector">
          <h1 class="selector">Select Currency</h1>
          <ul>
            <li class="name" v-for="(name, index) in names" :key="name" @click="getIndex(index)">{{ name }}</li>
         </ul>
        </div>
         <input type="text" class="header" placeholder="Enter Amount" v-model="amount" @keyup="getAmount"/>

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
      selectedName:0,
      amount:null,
      output:null
    
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
 
      } catch (error) {
        console.log(error);
      }
    },
    getIndex(index){
      this.selectedName = index
      console.log(index)
    },
    // getAmount(){
    //   if(this.amount){
    //    let amount = this.amount
    //    console.log(amount)
    // };
    getAmount(){
      let amount = this.amount
      console.log(amount)
      
    }
 

  },
  
}
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

 .currency-selector{
  position: relative;

}
.selector{
  cursor: pointer;
} 


 ul {
  list-style: none;
  cursor: pointer;
  position: absolute;
  max-height: 24rem;
  display: flex;
  flex-direction: column;


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
