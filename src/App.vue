<template>
  <div id="app">
    <h1>{{ msg }}</h1>

    <input id="search-box" type="text">

    <div id="hits-container"></div>
  </div>
</template>

<script>
var algoliasearch = require('algoliasearch')
let instantsearch = require('instantsearch.js')

export default {
  data () {
    return {
      msg: 'Hello Vue!'
    }
  },
  ready: () => {
    /*
    var client = algoliasearch('6DLEN782G1', '6ca42b1a471f2cc5def1aa1fedd10257')
    var index = client.initIndex('dev_knowledges')

    index.search('git', function searchDone(err, content) {
      console.log(err, content);
    })
    */

    
    let search = instantsearch({
      appId: '6DLEN782G1',
      apiKey: '6ca42b1a471f2cc5def1aa1fedd10257',
      indexName: 'dev_knowledges'
    })

    // Add a searchBox widget
    search.addWidget(
      instantsearch.widgets.searchBox({
        container: '#search-box',
        placeholder: 'Search for knowledges'
      })
    )
    
    // Add a hits widget
    search.addWidget(
      instantsearch.widgets.hits({
        container: '#hits-container',
        hitsPerPage: 10
      })
    )

    search.start()
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
</style>
