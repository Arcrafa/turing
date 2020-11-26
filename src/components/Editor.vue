<template>

  <div>
    <AceEditor
        :fontSize="14"
        :showPrintMargin="true"
        :showGutter="true"
        :highlightActiveLine="true"
        mode="json"
        theme="monokai"
        :onChange="onChange"
        name="editor"
        :editorProps="{$blockScrolling: true}"
        :defaultValue="defecto"

    />

  </div>

</template>

<script>
var primerAutomata='{\n' +
    '  "ini": "Q0",\n' +
    '  "estados": [\n' +
    '    {\n' +
    '      "nombre": "Q0",\n' +
    '      "transiciones": [\n' +
    '        {\n' +
    '          "lee": [\n' +
    '            "a",\n' +
    '            "b"\n' +
    '          ],\n' +
    '          "escribe": "a",\n' +
    '          "mueve": "D",\n' +
    '          "cambia": "Q0"\n' +
    '        },\n' +
    '        {\n' +
    '          "lee": [\n' +
    '            " "\n' +
    '          ],\n' +
    '          "escribe": " ",\n' +
    '          "mueve": "D",\n' +
    '          "cambia": "DONE"\n' +
    '        }\n' +
    '      ]\n' +
    '    },\n' +
    '    {}\n' +
    '  ],\n' +
    '  "acept": "done"\n' +
    '}'
import {Ace as AceEditor} from 'vue2-brace-editor';

import 'brace/mode/javascript';
import 'brace/theme/monokai';

export default {
  name: 'Editor',
  data(){
    return{
    automata: {
      ini: 'Q0',
      estados: [
        {
          nombre: 'Q0',
          transiciones: [{
            lee: ['a', 'b'],
            escribe: 'a',
            mueve: 'D',
            cambia: 'Q0'
          }, {
            lee: [' '],
            escribe: ' ',
            mueve: 'D',
            cambia: 'DONE'
          }]
        }, {}
      ],
      acept: 'done',


    },
    defecto:primerAutomata
    }

  },
  components: {
    AceEditor,
  },
  $el: 'root',
  methods: {
    onChange(newValue) {
      //console.log(newValue)
      this.automata=JSON.parse(newValue);
      this.$emit('automata',this.automata)
    }
  }
}
</script>