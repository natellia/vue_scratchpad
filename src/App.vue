<template>
  <!-- <MyCalculator msg="Enter value to calculate"/> -->
  <MyToDo msg="Enter your goals here"/>
</template>

<script>
// import MyCalculator from './components/Calculator.vue'
import MyToDo from './components/ToDoList.vue'

export default {
  name: 'App',
  components: {
    // MyCalculator,
    MyToDo
  }
}
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
</style>
