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
    />

  </div>
</template>

<script>

import {Ace as AceEditor} from 'vue2-brace-editor';

import 'brace/mode/javascript';
import 'brace/theme/monokai';

export default {
  name: 'Editor',
  data: {
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
      acept: 'done'

    }
  },
  components: {
    AceEditor,
  },
  $el: 'root',
  methods: {
    onChange(newValue) {
      console.log('change', newValue);
    }
  }
}
</script>