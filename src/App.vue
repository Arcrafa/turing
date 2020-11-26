<template>
  <div id="app">
    <Editor></Editor>
    <Grafo></Grafo>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Editor from "@/components/Editor";
import Grafo from "@/components/Grafo";
export default {
  name: 'App',
  components: {
    //HelloWorld
    Editor,
    Grafo
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
