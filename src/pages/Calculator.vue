<template>
  <div class='calculator' onselectstart='return false'>
    <div class='display'>{{display}}</div>
    <div @click='clear' class='button darker'>C</div>
    <div @click='sign' class='button darker'>+/-</div>
    <div @click='percent' class='button darker'>%</div>
    <div @click='divide' class='button operator'>÷</div>
    <div @click='append(7)' class='button'>7</div>
    <div @click='append(8)' class='button'>8</div>
    <div @click='append(9)' class='button'>9</div>
    <div @click='multiply' class='button operator'>x</div>
    <div @click='append(4)' class='button'>4</div>
    <div @click='append(5)' class='button'>5</div>
    <div @click='append(6)' class='button'>6</div>
    <div @click='subtract' class='button operator'>-</div>
    <div @click='append(1)' class='button'>1</div>
    <div @click='append(2)' class='button'>2</div>
    <div @click='append(3)' class='button'>3</div>
    <div @click='add' class='button operator'>+</div>
    <div @click='append(0)' class='button zero button-bottom'>0</div>
    <div @click='decimal' class='button darker button-bottom'>.</div>
    <div @click='equal' class='button operator button-bottom'>=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      display: 0,
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.display = 0;
    },
    sign() {
      this.display =
        this.display < 0
          ? (this.display = this.display - this.display * 2)
          : (this.display = this.display - this.display * 2);
    },
    percent() {
      this.display = this.display / 100;
    },
    append(number) {
      if (this.operatorClicked === true) {
        this.display = '';
        this.operatorClicked = false;
      }
      this.display =
        this.display === 0
          ? (this.display = number)
          : '' + this.display + number;
    },
    decimal() {
      if (this.display.indexOf('.') === -1) {
        this.append('.');
      }
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    add() {
      this.operator = (a, b) => a + b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    equal() {
      this.display = this.operator(Number(this.previous), Number(this.display));
      this.previous = null;
      this.operatorClicked = true;
    }
  }
};
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 80vw;
  font-size: 2rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(10vh, auto);
  border: 5px solid rgb(248, 56, 162);
  box-shadow: -3px 3px 15px rgba(238, 33, 129, 0.4);
  line-height: 10vh;
}

.display {
  grid-column: 1 / 5;
  background: rgb(135, 213, 236);
  border: 1px solid rgb(81, 140, 158);
  border-top: 0;
  font-size: 2.5rem;
  cursor: default;
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 1rem;
}

.zero {
  grid-column: 1 / 3;
}

.button {
  background: hsl(335, 62%, 84%);
  background: linear-gradient(15deg,hsl(335, 62%, 84%) 0%, hsl(334, 47%, 75%) 100%);
  border: 1px solid rgb(43, 40, 40);
  cursor: pointer;
}

.button:active {
  outline:none;
  border: 1px solid #ffffff; 
  box-shadow: inset 0px 0px 5px #ffffff; 
  -moz-box-shadow: inset 0px 0px 5px #ffffff;
  -webkit-box-shadow: inset 0px 0px 5px #ffffff;
}

.button-bottom {
  border-bottom: 0;
}

.operator {
  background: hsl(335, 75%, 69%);
  background: linear-gradient(15deg,hsl(335, 75%, 69%) 0%, hsl(335, 87%, 70%) 100%);
}

.darker {
  background: hsl(335, 75%, 69%);
  background: linear-gradient(15deg, hsl(335, 75%, 69%) 0%, hsl(335, 87%, 70%) 100%);
}

@media only screen and (min-width: 768px) {
  .calculator {
    width: 50vw;
    grid-auto-rows: minmax(7.5vh, auto);
    line-height: 7.5vh;
  }
}

@media only screen and (min-width: 1024px) {
  .calculator {
    width: 30vw;
  }
}

@media only screen and (min-width: 1280px) {
  .calculator {
    width: 20vw;
  }
}

@media only screen and (min-width: 1600px) {
  .calculator {
    width: 15vw;
  }
}
</style>
