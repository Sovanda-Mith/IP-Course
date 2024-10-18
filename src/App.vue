<template>
  <div id="app">
    <div class="container">
      <table>
        <tr>
          <td colspan="5">
            <div id="screen">
              <span id="screen_top">M=0</span>
              <div id="screen_bottom">
                <!-- v-text is a directive that is used to replace the content of HTML tag with private data -->
                <!-- It will update the content automatically when data is changed. It is called data reactive -->
                <span v-text="inputNumber" id="operand1">0</span>
                <span id="operator"></span>
                <span id="operand2"></span>
              </div>
              <!-- <span id="screen_bottom">0</span> -->
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <MyButton symbol="MC" btnColor="warning" />
          </td>
          <td>
            <MyButton symbol="MR" btnColor="warning" />
          </td>
          <td>
            <MyButton symbol="M-" btnColor="warning" />
          </td>
          <td>
            <MyButton symbol="M+" btnColor="warning" />
          </td>
          <td>
            <MyButton btnColor="default">
              <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
            </MyButton>
          </td>
        </tr>
        <tr>
          <td>
            <MyButton symbol="7" btnColor="default" />
          </td>
          <td>
            <MyButton symbol="8" btnColor="default" />
          </td>
          <td>
            <MyButton symbol="9" btnColor="default" />
          </td>
          <td>
            <MyButton symbol="÷" btnColor="secondary" />
          </td>
          <td>
            <MyButton symbol="+/-" btnColor="default" />
          </td>
        </tr>
        <tr>
          <td>
            <MyButton symbol="4" btnColor="default" />
          </td>
          <td>
            <MyButton symbol="5" btnColor="default" />
          </td>
          <td>
            <MyButton symbol="6" btnColor="default" />
          </td>
          <td>
            <MyButton symbol="x" btnColor="secondary" />
          </td>
          <td>
            <MyButton symbol="-" btnColor="secondary" />
          </td>
        </tr>
        <tr>
          <td>
            <MyButton :symbol="1" btnColor="default" />
          </td>
          <td>
            <MyButton :symbol="2" btnColor="default" />
          </td>
          <td>
            <MyButton :symbol="3" btnColor="default" />
          </td>
          <td rowspan="2">
            <MyButton symbol="+" btnColor="secondary" />
          </td>
          <td rowspan="2">
            <MyButton symbol="=" btnColor="primary" />
          </td>
        </tr>
        <tr>
          <td rowspan="2">
            <MyButton symbol="C" btnColor="danger" />
          </td>
          <td rowspan="2">
            <MyButton symbol="0" btnColor="default" />
          </td>
          <td rowspan="2">
            <MyButton symbol="." btnColor="default" />
          </td>
        </tr>
      </table>
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
      inputNumber: 0,
    };
  },
  methods: {
    showNumber(number) {
      // Assign number when user click to the inputNumber data
      // To access private data from methods, use (this.)
      this.inputNumber = number;
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
</style>
