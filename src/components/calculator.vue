<template>
  <div class="calculator">
    <h1>{{ message }}</h1>
  
    <div class='operands'>
      <input type="text" v-model="op1">
      <input type="text" v-model="op2">
    </div>

    <div class="calculations">
      <button v-on:click="result = parseInt(op1) + parseInt(op2)">+</button>
      <button v-on:click="result = op1 - op2">-</button>
      <button v-on:click="mul">*</button>
      <button v-on:click="del">/</button>
      <button v-on:click="result = Math.pow(op1, op2)">^</button>
      <button v-on:click="result = Math.floor(op1/op2)">//</button>
    </div>

    <div class='result'>Результат: {{ result }}</div>

    <div class="claviatura">
      <input type="checkbox" id="checkbox" v-model="checked">
      <label for="checkbox">Клавиатура</label>
      <input type="radio" id="one" value="onePick" v-model="picked">
      <label for="one">Operand 1</label>
      <input type="radio" id="two" value="twoPick" v-model="picked">
      <label for="two">Operand 2</label>
      <div class="clavishi" v-if='checked'>
        <button v-for="(num, idnum) in masNumber" :key="idnum" @click="clac(num)">{{num}}</button>
        <button v-html="backspace" @click="back"></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'calculator',
  props: {
    msg: String,
  },
  data() {
    return {
      message: 'Калькулятор',
      op1: '',
      op2: '',
      result: '-',
      masNumber: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      checked: false,
      picked: 'onePick',
      backspace:"&larr;"
    }
  },
  methods: {
    mul() {
      this.result = this.op1 * this.op2;
    },
    del() {
      const {op1, op2} = this
      this.result = op1 / op2;
    },
    clac(num) {
      if (this.picked === 'onePick') this.op1 +=num;
      else this.op2 +=num;
    },
    back() {
      if (this.picked === 'onePick') this.op1 = this.op1.slice(0, -1);
      else this.op2 = this.op2.slice(0, -1);
    }
  },
}
</script>

<style scoped lang="scss">
  .calculator {
    display: flex;
    flex-direction: column;
    max-width: 30%;
    & > div {
      margin-top: 20px;
    }
  }
  .operands {
    display: flex;
    justify-content: space-evenly;
  }
  .calculations {
    display: flex;
    justify-content: space-around;
  }
  .result {
    background-color: #5ccfd3;
    padding: 10px;
    display: flex;
    align-items: center;
    justify-content: space-around;
  }
  .clavishi {
    display: flex;
    justify-content: space-evenly;
    & div {
      border: 1px solid #000;
      padding: 10px 15px;
    }
  }
</style>
