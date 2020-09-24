<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div id="editor">
      <div>
        Editor 组件示例
      </div>
      <div>
        <Editor
          v-model="editorValue"
          height="240px"
          @init="editorInit"
          @setCompletions="setCompletions"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Editor from './components/Editor'

export default {
  name: 'App',
  components: {
    Editor
  },
  data() {
    return {
      editorValue: 'select * from mysql.user;',
      wordList: [
        {
          'vl': 'user01',
          'meta': '关键字'
        },
        {
          'vl': 'user',
          'meta': '表名'
        }
      ]

    }
  },
  methods: {
    editorInit: function() {
      require('brace/mode/mysql')
      require('brace/theme/xcode')
    },
    setCompletions(editor, session, pos, prefix, callback) {
      callback(null, this.wordList.map(function(word) {
        return {
          caption: word.vl,
          value: word.vl,
          meta: word.meta
        }
      }))
    },
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
#editor {
  /* display: flex; */
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 70%;
  padding-left: 15%;
}

</style>
