<script>

export default {
  data() {
    return {
      lastPressed:'',
      currentNumber: '',
      operator: null,
      firstOperand: null,
      secondOperand: null,
      waitingForSecondOperand: false,
      render: '',
      isAnswered: false,
    };
  },
  methods: {
    appendNumber(number) {
      if (this.isAnswered){
        this.render = ''
        this.isAnswered = false;
      }
      this.currentNumber = this.currentNumber.concat(number);
      this.render = this.render.concat(number);
      this.lastPressed = number;
      console.log(this.lastPressed);
    },

    perfomOperation(){
      this.secondOperand = this.currentNumber;
      console.log(this.secondOperand);
      if (this.operator != ''){
        this.render = '';
        switch (this.operator) {
            case '-':
              this.currentNumber = String(this.firstOperand - Number(this.secondOperand));
              break;
            case '+':
              this.currentNumber = String(this.firstOperand + Number(this.secondOperand));
              break;
            case '*':
              this.currentNumber = String(this.firstOperand * Number(this.secondOperand));
              break;
            case '/':
              this.currentNumber = String(this.firstOperand / Number(this.secondOperand));
              break;
        }}
      this.render = this.currentNumber;
      this.isAnswered = true;
      this.operator = null;
      this.firstOperand = null;
      this.secondOperand = null;
      this.currentNumber = '';
    },

    decide(op){
      if (!'+-/*'.includes(this.lastPressed)){
        if (this.operator != ''){
          this.render = this.render.concat(op);
          this.firstOperand = Number(this.currentNumber);
          this.currentNumber = '';
          this.waitingForSecondOperand = true;
          } else {
            this.perfomOperation();
          }
      }
      this.lastPressed = op;
      this.operator = op ;
    },
    cancel(){
      this.render = '';
      this.firstOperand = '';
      this.secondOperand = '';
      this.isAnswered = false;
      this.operator = '';
    }
  }
  
}

</script>

<template>

  <div class="calc">
    <div class="answer">{{ render }}</div>
    <div class="numpad">
        <button class="number" v-on:click="appendNumber('7')" >7</button>
        <button class="number" v-on:click="appendNumber('8')">8</button>
        <button class="number" v-on:click="appendNumber('9')">9</button>
        <button class="number" v-on:click="decide('*')">*</button>
        <button class="number" v-on:click="appendNumber('4')" >4</button>
        <button class="number" v-on:click="appendNumber('5')" >5</button>
        <button class="number" v-on:click="appendNumber('6')" >6</button>
        <button class="number" v-on:click="decide('/')">/</button>
        <button class="number" v-on:click="appendNumber('1')" >1</button>
        <button class="number" v-on:click="appendNumber('2')" >2</button>
        <button class="number" v-on:click="appendNumber('3')" >3</button>
        <button class="number" v-on:click="decide('-')">-</button>
        <button class="number" v-on:click="cancel()">c</button>
        <button class="number" v-on:click="appendNumber('0')" >0</button>
        <button class="number" v-on:click="perfomOperation()">=</button>
        <button class="number" v-on:click="decide('+')">+</button>
    </div>
</div>

</template>

<style>
.answer{
  width:400px;
  height:100px;
  background-color:bisque;
  color:black;
  margin:auto;
  position:relative;
  text-align:right;
  vertical-align: bottom;

}
.buffer{
 width:100px;
 background-color: rgb(174, 174, 174);
 display: inline-block;
}
.number{
 width: 100px;
 height: 100px; 
 background-color: aliceblue;
 color:black;
 position: relative;
 display: inline-block;

}
.calc{
  width:400px;
}
.numpad{
  display: block;
  background-color: grey;
  height: 400px;
  width:400px;
  align-items: stretch;
}
</style>
