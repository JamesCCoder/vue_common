<template>
  <div class="calculator">
    <div class="display">{{ current }}</div>
    <div class="buttons">
      <button @click="clear">C</button>
      <button @click="append('.')">.</button>
      <button @click="append('0')">0</button>
      <button @click="operate('/')">/</button>

      <button @click="append('1')">1</button>
      <button @click="append('2')">2</button>
      <button @click="append('3')">3</button>
      <button @click="operate('*')">*</button>

      <button @click="append('4')">4</button>
      <button @click="append('5')">5</button>
      <button @click="append('6')">6</button>
      <button @click="operate('-')">-</button>

      <button @click="append('7')">7</button>
      <button @click="append('8')">8</button>
      <button @click="append('9')">9</button>
      <button @click="operate('+')">+</button>

      <button @click="calculate">=</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      current: '',
      operator: null,
      previous: null
    };
  },
  methods: {
    append(number) {
      if (this.current === '' && number === '.') {
        this.current = '0.';
      } else {
        this.current += number;
      }
    },
    clear() {
      this.current = '';
      this.operator = null;
      this.previous = null;
    },
    operate(operator) {
      if (this.current === '') return;
      if (this.previous !== null) {
        this.calculate();
      }
      this.operator = operator;
      this.previous = this.current;
      this.current = '';
    },
    calculate() {
      let result;
      const previous = parseFloat(this.previous);
      const current = parseFloat(this.current);

      if (isNaN(previous) || isNaN(current)) return;

      switch (this.operator) {
        case '+':
          result = previous + current;
          break;
        case '-':
          result = previous - current;
          break;
        case '*':
          result = previous * current;
          break;
        case '/':
          result = previous / current;
          break;
        default:
          return;
      }

      this.current = result.toString();
      this.operator = null;
      this.previous = null;
    }
  }
};
</script>

<style scoped>
.calculator {
  width: 200px;
  margin: 100px auto;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.display {
  width: 100%;
  height: 40px;
  line-height: 40px;
  background: #f3f3f3;
  margin-bottom: 10px;
  font-size: 24px;
  text-align: right;
  padding-right: 10px;
  border-radius: 3px;
}

.buttons {
  display: flex;
  flex-wrap: wrap;
}

button {
  width: 25%;
  height: 40px;
  font-size: 18px;
  border: none;
  outline: none;
  cursor: pointer;
  background: #f3f3f3;
  transition: background 0.3s;
}

button:hover {
  background: #ddd;
}

button:nth-child(4n) {
  background: #f39c12;
  color: white;
}

button:nth-child(4n):hover {
  background: #e67e22;
}
</style>
