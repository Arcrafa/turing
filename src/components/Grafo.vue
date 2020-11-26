<template>
  <div>
    <h1>grafo</h1>
    <div id="mynetwork"></div>
  </div>
</template>

<script>
export default {
  name: "Grafo",
  data: {},


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
      console.log(network)
    }
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
