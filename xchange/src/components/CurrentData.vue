<template>
  <div class="main-container">
    <main class="exchange">
      <section class="currency-requested">

        <div class="currency-selector">
          <div class="selection-box">
           <div class="ul">
             <li class="name" v-for="(name, index) in names" :key="name" @click="getIndex(index)" >{{ name }}</li>
          </div>
           <h1 class="selector"  @click="active">Select Currency</h1>
         </div>
        </div>
         <input type="text" class="header" placeholder="Enter Amount" v-model="amount" @keyup="calcOutput" />

      </section>
      <section class="currency-returned">
           <div class="currency-selector">
          <div class="selection-box2">
            <div class="ul2">
            <li class="name" v-for="(name, index2) in names" :key="name" @click="getIndex2(index2)">{{ name }}</li>
           </div>
            <h1 class="selector2" @click="active2">Select Currency</h1>
         </div>
        </div>
    <input type="text" class="header" placeholder="Enter Amount" @keyup="calcInput" v-model="output"/>
      </section>

      
    </main>
    <h1>All Outputs are rounded to 3 decimals!</h1>
    <main class="reset">
      <button class="reset-button" @click="reset">Reset</button>
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
      selectedName2:0,
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
        console.log(this.result[8])
 
      } catch (error) {
        console.log(error);
      }
    },
    getIndex(index, e){
      this.selectedName = index
      const selector = document.querySelector(".selector")
      const allNames = document.querySelectorAll(".name")
       selector.innerHTML = e.innerHTML 
      allNames.classList.remove("active")
    },
    getIndex2(index2){
      this.selectedName2 = index2
      console.log(index2, this.selectedName)
      console.log(this.result[this.selectedName])
    },
    getAmount(){
       let amount = this.amount
       console.log(this.result[this.selectedName])
       console.log(amount)
  },
  calcOutput(){
      this.output = ((this.amount/this.result[this.selectedName])*this.result[this.selectedName2]).toFixed(3)
      console.log(this.output)
    },
    calcInput(){
      this.amount = ((this.output/this.result[this.selectedName2])*this.result[this.selectedName]).toFixed(3)
    },
    reset(){
    this.amount = null
    this.output = null
    },
    active(){
      const ul = document.querySelector(".ul")
      ul.classList.toggle("active")
    },
      active2(){
      const ul2 = document.querySelector(".ul2")
      ul2.classList.toggle("active")
    },
    rename(e){
      const selector = document.querySelector(".selector")
      const allNames = document.querySelectorAll(".name")
      selector.innerHTML = e.innerHTML 
      allNames.classList.remove("active")
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
  height: 50%;

}
.selector{
  cursor: pointer;
  background: #2f3640;
  border-radius: 0.8rem;
  margin-bottom: 0.8rem;
  color: white;
  position: relative;

  order: 0;
} 

.selector2{
  cursor: pointer;
  background: #2f3640;
  border-radius: 0.8rem;
  margin-bottom: 0.8rem;
  color: white;
  position: relative;

  order: 0;
} 
.selection-box{
  display: flex;
  width: 20rem;
  flex-direction: column;
}
.selection-box2{
  display: flex;
  width: 20rem;
  flex-direction: column;
}

.selection-box .ul {
  display: flex;
  flex-direction: column;
  background: #2f3640;
  color: white;
  max-height: 0;
  width: 100%;
  opacity: 0;
  transition: all 0.4s;
  border-radius: 8px;
  overflow: hidden;
  list-style: none;

  order: 1;
}

.selection-box2 .ul2 {
  display: flex;
  flex-direction: column;
  background: #2f3640;
  color: white;
  max-height: 0;
  width: 100%;
  opacity: 0;
  transition: all 0.4s;
  border-radius: 8px;
  overflow: hidden;
  list-style: none;

  order: 1;
}
.selection-box .ul.active{
  max-height: 10rem;
  overflow-y: scroll;
  opacity: 1;
}

.selection-box2 .ul2.active{
  max-height: 10rem;
  overflow-y: scroll;
  opacity: 1;
}

.selection-box .ul::-webkit-scrollbar{
  width: 0.8rem;
  background: #0d141f;
  border-radius: 0 0.8rem 0.8rem 0;
}

.selection-box2 .ul2::-webkit-scrollbar{
  width: 0.8rem;
  background: #0d141f;
  border-radius: 0 0.8rem 0.8rem 0;
}

.selection-box .ul::-webkit-scrollbar-thumb{
  background: #525861;
  border-radius: 0 0.8rem 0.8rem 0;
}

.selection-box2 .ul2::-webkit-scrollbar-thumb{
  background: #525861;
  border-radius: 0 0.8rem 0.8rem 0;
}
.selection-box .name,
.selector {
  padding: 0.6rem 1.4rem;
  cursor: pointer;
}

.selection-box2 .name,
.selector2 {
  padding: 0.6rem 1.4rem;
  cursor: pointer;
}


.selection-box .name:hover{
  background: #414b57;
}

.selection-box2 .name:hover{
  background: #414b57;
}
 /* ul {
  list-style: none;
  cursor: pointer;
  position: absolute;
  max-height: 9rem;
  width: 15rem;
  display: flex;
  flex-direction: column;
  overflow-y: scroll;
  transform: translateX(-20%);
  text-align: left;
  border: 1px black solid;
   display: none; 

}  */

/* li:hover{
  background-color: rgb(189, 189, 189);
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
