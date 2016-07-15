<template>
  <div id="app">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
var algoliasearch = require('algoliasearch')

export default {
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      msg: 'Hello Vue!'
    }
  },
  created: () => {
    var client = algoliasearch('6DLEN782G1', '6ca42b1a471f2cc5def1aa1fedd10257')
    var index = client.initIndex('dev_knowledges')

    index.search('git', function searchDone(err, content) {
      console.log(err, content);
    })
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
</style>
