<template>
  <div id="app">
  <Header class="marginBottom"/>
   <QuantityInput 
   v-bind:value="value" 
   v-bind:selectMin="selectMin" 
   v-bind:selectMax="selectMax" 
   v-on:new-value-selected="customValueInputted"/>
  </div>
</template>

<script>
import QuantityInput from "./components/QuantityInput";
import Header from "./components/Header";

export default {
  name: "app",
  components: {
    QuantityInput,
    Header
  },
  data() {
    return {
      value: 8,
      selectMin: 4,
      selectMax: 10
    };
  },
  methods: {
    customValueInputted(value) {
      // eslint-disable-next-line
      console.log(`Inputted value is: ${value}`);
    }
  }
};
</script>

<style>
#app {
  left: 10%;
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.marginBottom {
  margin-bottom: 2%;
}
</style>
