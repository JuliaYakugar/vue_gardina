<template>
  <div class="calculator">
    <h1>{{ message }}</h1>
  
    <div class='operands'>
      <input type="number" v-model.number="op1">
      <input type="number" v-model.number="op2">
    </div>

    <div class="calculations">
      <button v-on:click="result = op1 + op2">+</button>
      <button v-on:click="result = op1 - op2">-</button>
      <button v-on:click="mul">*</button>
      <button v-on:click="del">/</button>
      <button v-on:click="result = Math.pow(op1, op2)">^</button>
      <button v-on:click="result = Math.floor(op1/op2)">//</button>
    </div>

    <div class='result'>Результат: {{ result }}</div>
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
      op1: 0,
      op2: 0,
      result: 0,
    }
  },
  methods: {
    mul() {
      this.result = this.op1 * this.op2;
    },
    del() {
      const {op1, op2} = this
      this.result = op1 / op2;
    }
  },
}
</script>

<style scoped lang="scss">
  .calculator {
    display: flex;
    flex-direction: column;
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
</style>
