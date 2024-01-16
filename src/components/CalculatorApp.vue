<template>
    <div class="calculator">
      <div class="display">{{ display }}</div>
      <div class="buttons">
        <button v-for="button in buttons" :key="button" @click="handleClick(button)">
          {{ button }}
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        display: '0',
        buttons: ['7', '8', '9', '/', '4', '5', '6', '*', '1', '2', '3', '-', '0', '.', '=', '+'],
        operatorClicked: false,
      };
    },
    methods: {
      handleClick(button) {
        if (button === '=') {
          this.calculateResult();
        } else {
          this.updateDisplay(button);
        }
      },
      calculateResult() {
        try {
          this.display = eval(this.display).toString();
        } catch (error) {
          this.display = 'Error';
        }
        this.operatorClicked = false;
      },
      updateDisplay(value) {
        if (this.operatorClicked && isNaN(value)) {
          this.display += ' ' + value + ' ';
        } else {
          if (this.display === '0' || this.display === 'Error') {
            this.display = value;
          } else {
            this.display += value;
          }
        }
        this.operatorClicked = !isNaN(value);
      },
    },
  };
  </script>
  
  <style scoped>
  .calculator {
    max-width: 300px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  
  .display {
    font-size: 24px;
    margin-bottom: 10px;
    padding: 10px;
    text-align: right;
    border: 1px solid #ccc;
    border-radius: 3px;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  
  button {
    font-size: 18px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 3px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #eee;
  }
  </style>
  