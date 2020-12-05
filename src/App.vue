<template>
  <div>
    <div id="app" class="row container">
      <Editor @automata="getautomata" class="col s6"></Editor>
      <Grafo :automata="automata" :actual="estado_actual" class="col s6"></Grafo>

    </div>

    <div class="container">
      <form class="col s10">
        <div class="row">
          <h5>ingrese los simbolos de la cinta</h5>

          <div class="input-field col s12">
            <input id="textarea1" class="materialize-textarea" v-model="cinta_text"  >
            <button class="btn waves-effect waves-light" type="submit" name="action" @click="genCinta">cargar cinta

            </button>
          </div>
          <div class="col s2">
            <button class="btn waves-effect waves-light" type="submit" name="action" @click="evaluar">evaluar
              <i class="material-icons right">skip_next</i>
            </button>
          </div>
        </div>
      </form>
    </div>

    <div class="col s12">

      <table class="centered">
        <thead>
        <tr>
          <!--<div class="vl"></div>-->
          <th

              v-for="celda in cinta"
              :class=" celda.actual ? 'celda-cinta-actual' :  'celda-cinta'"
          >
            {{ celda.simbolo }}
          </th>
        </tr>
        </thead>
      </table>

    </div>
  </div>

</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Editor from "@/components/Editor";
import Grafo from "@/components/Grafo";

export default {
  name: 'App',
  data() {
    return {
      cinta_text:'',
      automata: null,
      estado_actual: '',
      cinta:[]
    }

  },
  components: {
    //HelloWorld
    Editor,
    Grafo
  }
  ,
  methods: {
    getautomata(automata) {
      this.automata = automata
      this.estado_actual = this.automata.init
    },
    evaluar(event) {

      if (event) {
        event.preventDefault()
      }
      if (this.estado_actual == '') this.estado_actual = this.automata.init


      var E = this.automata.estados.find(estado => estado.nombre = this.estado_actual)

      var T = E.transiciones.find(transicion => transicion.lee.includes(this.simbolo_actual))
      console.log(T.escribe)
      this.escribir(T.escribe)

      this.mover(T.mueve)

      this.estado_actual = T.cambia
      if (this.estado_actual == this.automata.acept) alert("operacion completada")
    },
    mover(direccion) {
      var actual = this.cinta.find(celda => celda.actual)
      var index = this.cinta.indexOf(actual)
      console.log(index)
      if (direccion == 'D') {
        this.cinta[index + 1].actual = true
      } else {
        this.cinta[index - 1].actual = true
      }

      this.cinta[index].actual = false
    },
    escribir(new_simbolo) {
      console.log(new_simbolo)
      var actual = this.cinta.find(celda => celda.actual)
      var index = this.cinta.indexOf(actual)
      console.log(index)
      this.cinta[index].simbolo = new_simbolo
      console.log(this.cinta)


    },
    genCinta (event){

      if (event) {
        event.preventDefault()
      }
      this.cinta_text+="   "
      var simbolos=this.cinta_text.split("")

      this.cinta=[]
      simbolos.forEach(sim=>{
        this.cinta.push({simbolo:sim,actual:false})
      })
      this.cinta[0].actual=true
      console.log(simbolos)
    }
  },

  computed: {
    // a computed getter
    simbolo_actual: function () {
      // `this` points to the vm instance
      return this.cinta.find(celda => celda.actual).simbolo
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


.horizontal {
  display: inline;
  margin-right: 5px;
  margin-left: 5px;
}

.vl {
  border-left: 1px solid green;
  height: 53px;
}

.celda-cinta {
  border: 1px solid green;
}

.celda-cinta-actual {
  border: 1px solid green;
  background-color: #42b983;
}
</style>
