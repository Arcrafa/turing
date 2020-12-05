<template>
  <div>
    <h4>grafo del automata</h4>
    <div id="mynetwork"></div>
    <h5> estado actual:{{this.actual}}</h5>
  </div>
</template>

<script>
export default {
  name: "Grafo",
  props: {
    automata: Object,
    actual:String
  },

  data() {
    return {
      estados: [],
      transiciones: []
    }
  },
  mounted() {
    this.grafo()
  },
  methods: {

    grafo: function (e) {
      console.log("dibujando")
      console.log(this.automata)

      this.estados = []
      this.transiciones = []
      var i = 1
      this.automata.estados.forEach(estado => {

        this.estados.push({id: i, label: estado.nombre})
        i++

      })


      this.automata.estados.forEach(estado => {

        if (estado.nombre != this.automata.accept) {

          estado.transiciones.forEach(transicion => {


            var l = transicion.lee.join(',') + '->' + transicion.escribe + ',' + transicion.mueve

            this.transiciones.push({
              from: this.estados.find((e) => e.label == estado.nombre).id,
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
  },
  updated() {

    this.grafo()
  }
}
</script>

<style escoped>
#mynetwork {
  height: 400px;
  border: 1px solid lightgray;
}
</style>
