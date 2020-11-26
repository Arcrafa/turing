<template>
  <div id="app">
    <Editor @automata="getautomata"></Editor>
    <Grafo :automata="automata"></Grafo>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Editor from "@/components/Editor";
import Grafo from "@/components/Grafo";
export default {
  name: 'App',
  data(){
    return {
      automata: null
    }

  },
  components: {
    //HelloWorld
    Editor,
    Grafo
  },
  methods:{
    getautomata(automata){
        this.automata=automata
    }
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
