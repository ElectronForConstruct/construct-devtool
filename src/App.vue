<template>
  <div id="app">
    <DevTool/>
  </div>
</template>

<script>
import DevTool from './components/DevTool.vue';

export default {
  name: 'app',
  components: {
    DevTool,
  },
};
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
