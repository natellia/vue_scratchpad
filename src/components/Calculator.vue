<template>
  <div class="calculator">
    <h1>{{ msg }}</h1>
    <div><input v-model='answer' readonly /></div>
    <div><input v-model='argumentSeen' readonly /></div>
    <div id="keypad">
      <template v-for="buttonText in this.buttons" v-bind:key="buttonText.id">
        <button class="calculatorButton" v-if="buttonText != 'b'" v-on:click="input(buttonText)">
          {{ buttonText }}
         </button>
        <span v-else>
          <br />
         </span>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyCalculator',
  props: {
    msg: String
  },
  data: function() {
    return {
      argumentUnseen: '',
      argumentSeen: '',
      answer: '',
      buttons: [
        '7', '8', '9', 'b',
        '4', '5', '6', 'b',
        '1', '2', '3', 'b',
        '0', '/', '=', 'b',
        '+', '-', '*', 'b',
        'C', 'CE', 'X', 'b'
      ],
      iterator: 0
    }
  },
  methods: {
    calculate(argumentUnseen) {
      try {
        var solution = eval(argumentUnseen);
      } catch(Exception) {
        this.answer = "ERR";
        this.argumentUnseen = "";
        this.argumentSeen = "";
      } 

      if(solution != "ERR") {
        this.argumentSeen = solution;
        this.answer = this.argumentUnseen + "=";
        this.argumentUnseen = solution;
      }
    },
    input(str) {
      if(str != "=" && str != "C" && str != "CE" && str != "+" && str != "-" && str != "*" && str != "/") {
        this.argumentUnseen += str;
        this.argumentSeen += str;
      }
      else if(str == "=") {
        this.calculate(this.argumentUnseen);
      }
      else if(str == "C") {
        this.clearAll();
      }
      else if(str == "CE") {
        if(this.answer.charAt(this.answer.length - 1) == "=") {
          this.clearAll();
        } else {
          this.argumentSeen = '';

          var argArray = this.argumentUnseen.split('');
          var numToRemove = '';
          for(var i = argArray.length - 1; i >= 0; i--) {
            if(!isNaN(argArray[i])) {
              numToRemove = argArray[i] + numToRemove;
            } else {
              this.argumentUnseen = this.argumentUnseen.replace(numToRemove, '');
              this.answer = this.argumentUnseen;
            }
          }
        }
      }
      else {
        this.answer = this.argumentUnseen + str;
        this.argumentSeen = '';
        this.argumentUnseen = this.answer;
      }
    },
    clearAll() {
      this.argumentUnseen = '';
      this.argumentSeen = '';
      this.answer = '';
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
div {
  padding: 30px;
}
.calculatorButton {
  height: 5rem;
  width: 5rem;
  justify-content: center;
  align-items: center;
  background-color: #008CBA;
  color: white;
  font-size: 16px;
}
</style>
