<template>
  <div id="app">
    <div class="container">
      <div>
        <div id="screen">
          <span id="screen_top">M=0</span>
          <div id="screen_bottom">
            <!-- v-text is a directive that is used to replace the content of HTML tag with private data -->
            <!-- It will update the content automatically when data is changed. It is called data reactive -->
            <span id="operand1">{{ lastInput || "0" }}</span>
            <span id="operator"></span>
            <span id="operand2"></span>
          </div>
          <!-- <span id="screen_bottom">0</span> -->
        </div>
      </div>
      <div id="keypad">
        <div class="normal">
          <MyButton symbol="MC" btnColor="warning" />
          <MyButton symbol="7" btnColor="default" @btn-click="append(7)" />
          <MyButton symbol="4" btnColor="default" @btn-click="append(4)" />
          <MyButton symbol="1" btnColor="default" @btn-click="append(1)" />
          <MyButton symbol="C" btnColor="danger" @btn-click="clearInput" />
        </div>
        <div class="normal">
          <MyButton symbol="MR" btnColor="warning" />
          <MyButton symbol="8" btnColor="default" @btn-click="append(8)" />
          <MyButton symbol="5" btnColor="default" @btn-click="append(5)" />
          <MyButton symbol="2" btnColor="default" @btn-click="append(2)" />
          <MyButton symbol="0" btnColor="default" @btn-click="append(0)" />
        </div>
        <div class="normal">
          <MyButton symbol="M-" btnColor="warning" />
          <MyButton symbol="9" btnColor="default" @btn-click="append(9)" />
          <MyButton symbol="6" btnColor="default" @btn-click="append(6)" />
          <MyButton symbol="3" btnColor="default" @btn-click="append(3)" />
          <MyButton symbol="." btnColor="default" @btn-click="dot" />
        </div>
        <div class="normal">
          <MyButton symbol="M+" btnColor="warning" />
          <MyButton symbol="÷" btnColor="secondary" @btn-click="divide" />
          <MyButton symbol="x" btnColor="secondary" @btn-click="multiply" />
          <MyButton
            symbol="+"
            btnColor="secondary"
            class="expand"
            @btn-click="add"
          />
        </div>
        <div class="normal">
          <MyButton symbol="" btnColor="default" @btn-click="backspace">
            <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
          </MyButton>
          <MyButton symbol="+/-" btnColor="default" @btn-click="sign" />
          <MyButton symbol="-" btnColor="secondary" @btn-click="subtract" />
          <MyButton
            symbol="="
            btnColor="primary"
            class="expand"
            @btn-click="equal"
          />
        </div>
      </div>
    </div>
    <div class="alert alert-danger" id="message_panel" role="alert">
      something wrong here
    </div>
  </div>
</template>

<script>
import MyButton from "./components/MyButton.vue";
export default {
  name: "App",
  components: {
    MyButton,
  },
  data() {
    return {
      // This is the private data section which can be used inside this component
      previousInput: null,
      lastInput: "",
      operator: null,
      operatorClick: false,
    };
  },
  methods: {
    clearInput() {
      this.lastInput = "";
    },
    sign() {
      this.lastInput =
        this.lastInput.charAt(0) === "-"
          ? this.lastInput.slice(1)
          : `-${this.lastInput}`;
    },
    showNumber(number) {
      // Assign number when user click to the inputNumber data
      // To access private data from methods, use (this.)
      this.inputNumber = number;
    },
    setPrevious() {
      this.previousInput = this.lastInput;
      this.operatorClick = true;
    },
    append(symbol) {
      if (this.operatorClick) {
        this.lastInput = "";
        this.operatorClick = false;
      }
      this.lastInput = `${this.lastInput}${symbol}`;
    },
    dot() {
      if (this.lastInput.indexOf(".") === -1) {
        this.append(".");
      }
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    equal() {
      this.lastInput = `${this.operator(
        parseFloat(this.previousInput),
        parseFloat(this.lastInput)
      )}`;
      this.previousInput = null;
    },
    backspace() {
      this.lastInput = this.lastInput.slice(0, -1);
    },
  },
};
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
.container {
  margin-top: 10em;
  width: 300px;
  border: 1px solid black;
  padding-top: 20px;
  padding-bottom: 20px;
}
table {
  border-spacing: 7px;
  border-collapse: separate;
}
#screen {
  border: 1px solid black;
  padding: 7px;
  width: 100%;
  height: 4em;
}
#screen_top {
  display: block;
  font-size: 0.8rem;
}
#screen_bottom {
  font-size: 1.8rem;
  display: block;
  text-align: right;
}
#operand2 {
  background-color: skyblue;
}
#operator {
  background-color: rosybrown;
}
.button-row {
  display: flex;
  justify-content: space-between;
}
button {
  width: 45px;
}
.long-btn {
  display: inline-block;
  height: 80px;
}

/* Message panel */
#message_panel {
  width: 300px;
  margin-top: 1em;
  display: none;
  margin-left: auto;
  margin-right: auto;
}

#keypad {
  display: flex;
  margin-top: 10px;
  column-gap: 10px;
}

.normal {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.expand {
  flex-grow: 1;
}
</style>
