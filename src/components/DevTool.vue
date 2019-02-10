<template>
  <div id="devtool">
    <div class="bubble">
      cog
    </div>
    <div class="modal">
      <button @click="reloadWindow">Reload</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DevTool',
  methods: {
    reloadWindow() {
      const event = new Event('reloadPage');
      document.dispatchEvent(event);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #devtool {
    position: fixed;
    right: 0;
    bottom: 0;
  }

  .bubble {
    background-color: #005fff;
    height: 50px;
    width: 50px;
    line-height: 50px;
    text-align: center;
    border-radius: 25px;
    color: #fff;
    cursor: pointer;
  }
</style>
