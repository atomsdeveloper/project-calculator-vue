<template>
  <div id="app">
    <h1> Calculadora </h1>
    <CalculatorCustom />
  </div>
</template>


<!-- JS -->
<script>
import CalculatorCustom from "./main/CalculatorCustom.vue"

export default {
  components: { CalculatorCustom }
}
</script>


<!-- CSS -->
<style>
@font-face {
  font-family: "Ubuntu";
  src: url("./fonts/Ubuntu-Light.ttf");
}

* {
  font-family: "Ubuntu", monospace;
}

body {
  margin: 0;
}

#app {
  height: 100vh;

  display: flex;
  text-align: center;
  align-items: center;
  flex-direction: column;
  justify-content: center;

  color: black;
}
</style>
