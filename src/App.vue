<template>
  <div id="app">
    
    <todoElement></todoElement>

  </div>
</template>

<script>
import todoElement from "./components/todoElement";

export default {
  name: 'App',
  components: {

    todoElement,

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
<style lang="less" scoped>

</style>