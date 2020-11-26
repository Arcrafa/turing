<template>
  <div>
    <h1>grafo</h1>
    <div id="mynetwork"></div>
    {{automata}}
  </div>
</template>

<script>
export default {
  name: "Grafo",
  props:{
    automata:Object
  },

  data(){
    return{
      estados:[],
      transiciones:[]
    }
  },
  mounted() {
    this.grafo()
  },
  methods: {
    idEstado:function (nombre){

      console.log(this.estados.find(estado => estado.nombre == nombre));

    },
    grafo: function (e) {
      // create an array with nodes
      var nodes = new vis.DataSet([
        {id: 1, label: 'QO'},
        {id: 2, label: 'aceptacion'},

      ]);

      // create an array with edges
      var edges = new vis.DataSet([
        {from: 1, to: 1, arrows: "to", label: "a,b -> a,R", font: {align: "bottom"}},
        {from: 1, to: 2, arrows: "to", label: "' ',-> R", font: {align: "bottom"}}
      ]);

      // create a network
      var container = document.getElementById('mynetwork');

      // provide the data in the vis format
      var data = {
        nodes: nodes,
        edges: edges
      };
      var options = {};

      // initialize your network!
      var network = new vis.Network(container, data, options);
      console.log(network)
    }
  },
  updated() {
    var indice={

    }

    var i=1
    this.automata.estados.forEach(estado=>{

      this.estados.push({id: i, label:estado.nombre })
      i++

    })
    i=1
    this.automata.estados.forEach(estado=>{
      i++
      estado.transiciones.forEach(transicion=>{

        var l=transicion.lee.join(',')+'->'+ transicion.escribe+','+transicion.mueve
        console.log(this.idEstado(estado.nombre))
        this.transiciones.push({from: this.idEstado(estado.nombre), to: this.idEstado(transicion.cambia), arrows: "to", label: l, font: {align: "bottom"}})
      })

    })
    console.log(this.automata)
  }
}
</script>

<style escoped>
#mynetwork {
  width: 600px;
  height: 400px;
  border: 1px solid lightgray;
}
</style>
