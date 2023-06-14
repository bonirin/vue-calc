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
      answer: null,
      isAnswered: false,
    };
  },
  methods: {
    appendNumber(number) {
      this.currentNumber = this.currentNumber.concat(number);
      this.render = this.render.concat(number);
      this.lastPressed = number;
      this.isAnswered = false;
    },

    perfomOperation(){
      this.answer = '';
      this.secondOperand = Number(this.currentNumber);
      if (this.operator != null){
        console.log(this.operator)
        console.log(this.firstOperand)
        console.log(this.secondOperand)
        this.render = '';
        switch (this.operator) {
            case '-':
              this.answer = this.firstOperand - this.secondOperand;
              break;
            case '+':
              this.answer = this.firstOperand + this.secondOperand;
              break;
            case '*':
              this.answer = this.firstOperand * this.secondOperand;
              break;
            case '/':
              this.answer = this.firstOperand / this.secondOperand;
              break;
        }}
      console.log(this.answer)
      this.render = String(this.answer);
      this.firstOperand = this.answer
      this.secondOperand = null;
      this.isAnswered = true
    },

    decide(op){
      if (('+-/*'.includes(this.lastPressed)) && this.operator != null){
        this.render = this.render.slice(0,-1);
      }
      if ((!'+-/*'.includes(this.lastPressed)) && (this.operator != null) && (!this.isAnswered)){
        this.perfomOperation()
      }
      if (this.isAnswered){
        this.firstOperand = this.answer
      } else {
        this.firstOperand = Number(this.currentNumber)
      }
      this.lastPressed = op;
      this.operator = op;
      this.render = this.render.concat(op);
      // if (this.operator != null){
      //     this.perfomOperation();
      //     this.render = this.currentNumber;
      // }
      // this.render = this.render.concat(op);
      this.currentNumber = '';
      // console.log(this.firstOperand);
      // this.waitingForSecondOperand = true;
    },
    cancel(){
      this.render = '';
      this.firstOperand = null;
      this.secondOperand = null;
      this.isAnswered = false;
      this.operator = null;
      this.currentNumber = '';
      this.lastPressed = '';
    }
  }
  
}

</script>

<template>

  <div class="calc">
    <div class="answer">{{ render }}</div>
    <div class="numpad">
        <button v-on:click="appendNumber('7')" >7</button>
        <button v-on:click="appendNumber('8')">8</button>
        <button v-on:click="appendNumber('9')">9</button>
        <button v-on:click="decide('*')">*</button>
        <button v-on:click="appendNumber('4')" >4</button>
        <button v-on:click="appendNumber('5')" >5</button>
        <button v-on:click="appendNumber('6')" >6</button>
        <button v-on:click="decide('/')">/</button>
        <button v-on:click="appendNumber('1')" >1</button>
        <button v-on:click="appendNumber('2')" >2</button>
        <button v-on:click="appendNumber('3')" >3</button>
        <button v-on:click="decide('-')">-</button>
        <button v-on:click="cancel()">c</button>
        <button v-on:click="appendNumber('0')" >0</button>
        <button v-on:click="perfomOperation()">=</button>
        <button v-on:click="decide('+')">+</button>
    </div>
</div>

</template>

<style>
.answer{
  height:100px;
  background-color:bisque;
  color:black;
  margin:auto;
  position:relative;
  text-align:right;
  vertical-align: bottom;
  font-size: 50px;

}
.buffer{
 background-color: rgb(174, 174, 174);
 display: inline-block;
}
.calc{
  width:400px;
  height: 500px;
}
.numpad{
  height: 400px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr;
  background-color: grey;
}
</style>
