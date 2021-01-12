<template>
  <div id="app">
    <my-list id = "demo" msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import MyList from './components/MyList.vue'

export default {
  name: 'App',
  components: {
    MyList
  }
}
</script>

<style>
#app {
  /*display: inline-block;*/
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#demo{
  position: relative;
  top:200px;
  margin: 0 auto;
}
</style>
