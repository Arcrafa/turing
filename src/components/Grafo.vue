<template>
  <div>
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
    }
  },
  updated() {

    this.estados=[]
    this.transiciones=[]
    var i=1
    this.automata.estados.forEach(estado=>{

      this.estados.push({id: i, label:estado.nombre })
      i++

    })


    this.automata.estados.forEach(estado=>{

      if (estado.nombre!=this.automata.accept) {

      estado.transiciones.forEach(transicion=>{


          var l = transicion.lee.join(',') + '->' + transicion.escribe + ',' + transicion.mueve

          this.transiciones.push({
            from: this.estados.find((e) => e.label ==estado.nombre).id,
            to: this.estados.find((e) => e.label == transicion.cambia).id,
            arrows: "to",
            label: l,
            font: {align: "bottom"}
          })

      })

        }

    })
    // create an array with nodes
    var nodes = new vis.DataSet(this.estados);

    // create an array with edges
    var edges = new vis.DataSet(this.transiciones);
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
