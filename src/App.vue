<template>
 <h1>Simple Calculator Using Vue</h1>
<div class="calculator">
 
  <div class="display">
   {{current || '0'}}
  </div>
  
  <div @click="clear" class="btn">AC</div>
  <div @click="sign" class="btn">+/-</div>
  <div class="btn" @click="percent" >%</div>
  <div @click="divide" class="btn operator" >/</div>
  <div @click="append(1)" class="btn">1</div>
  <div @click="append(2)" class="btn">2</div>
  <div @click="append(3)" class="btn">3</div>
  <div @click="times" class="btn operator">X</div>
  <div @click="append(4)" class="btn">4</div>
  <div @click="append(5)" class="btn">5</div>
  <div @click="append(6)" class="btn">6</div>
  <div @click="minus" class="btn operator">-</div>
  <div @click="append(7)" class="btn">7</div>
  <div @click="append(8)" class="btn">8</div>
  <div @click="append(9)" class="btn">9</div>
  <div @click="add" class="btn operator">+</div>
  <div @click="append(0)" class="btn zero">0</div>
  <div @click="dot" class="btn">.</div>
  <div @click="equal" class="btn operator">=</div>
  
  </div>
</template>

<script>



export default {
  name: 'App',
  data(){
   return{
     current:'',
     operator:null,
     previous:null,
     operatorClicked:false,


   }
  },

  methods:{
    clear(){
      this.current=''
    },
    sign(){
      this.current = this.current.charAt(0)==='-'? this.current.slice(1):`-${this.current}`

    },
    percent(){
      this.current = `${parseFloat(this.current)/100}`
    },
  append(number){
    if(this.operatorClicked){
      this.current=''
      this.operatorClicked=false
    }
    this.current = `${this.current}${number}`
  },
  dot(){
    if(this.current.indexOf('.')===-1){
      this.append('.')
    }

  },
  setPrevious(){
    this.previous=this.current;
    this.operatorClicked=true;
   
  },
  add(){
    this.operator=(a,b)=>a+b;
    this.setPrevious();
  },
  minus(){
    this.operator=(a,b)=>a-b;
   this.setPrevious();

  },
  times(){
    this.operator=(a,b)=>a*b;
        this.setPrevious();

  },
  divide(){
    this.operator=(a,b)=>a/b;
        this.setPrevious();

  },
  equal(){
    this.current=`${this.operator(parseFloat(this.previous),parseFloat(this.current))}`

  }
    
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.calculator{
  margin: 0 auto;
  width: 400px;
  font-size: 20px;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px,auto);
}
h1{
  font-size: 35px;
  color: deepskyblue;
}
.display{
  border: 1px solid black;
  grid-column: 1/5;
  background: blueviolet;
  color: white;
  padding-top: 10px;
  

}
.zero{
  grid-column: 1/3;
}
.btn{
    padding-top: 10px;

  background-color: #eee;
  border: 1px solid #3333;
}
.operator{
  background: orange;
}
</style>
