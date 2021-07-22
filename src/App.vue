<template>
  <div id="app"></div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  position: absolute;
  left: 0;
  top: 0;
  overflow-x: hidden;
  width: 100vw;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out;
}
</style>
