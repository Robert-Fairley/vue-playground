<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Doc componentTitle="Test" />
    <!--<HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>-->
    <Counter count=0 />
    <Name />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import Counter from './components/Counter.vue';
import Name  from './components/Name.vue';
import Doc from './components/Doc.vue';

require("./assets/vue-nestable.css");

@Component({
  components: {
    //HelloWorld,
    Doc,
    Counter,
    Name,
  },
})
export default class App extends Vue {}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
