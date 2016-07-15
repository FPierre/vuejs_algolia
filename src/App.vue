<template>
  <div id="app">
    <h1>{{ msg }}</h1>

    <input id="search-input" type="text">

    <div id="hits-container"></div>
  </div>
</template>

<script>
let algoliasearch = require('algoliasearch')
// let instantsearch = require('instantsearch.js')
let autocomplete = require('../vendor/autocomplete.min.js')

export default {
  data () {
    return {
      msg: 'Hello Vue!'
    }
  },
  ready: () => {
    var client = algoliasearch('6DLEN782G1', '6ca42b1a471f2cc5def1aa1fedd10257')
    var index = client.initIndex('dev_knowledges')

    /*
    index.search('git', function searchDone(err, content) {
      console.log(err, content);
    })
    */

    /*
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
    */

    autocomplete('#search-input', { hint: false }, [
      {
        source: autocomplete.sources.hits(index, { hitsPerPage: 5 }),
      	displayKey: 'tags',
        templates: {
          suggestion: function (suggestion) {
            return suggestion._highlightResult.tags.value
          }
        }
      }
    ]).on('autocomplete:selected', function (event, suggestion, dataset) {
      console.log(suggestion, dataset)
    })
  }
}
</script>

<style>
.algolia-autocomplete {
  width: 100%;
}

.algolia-autocomplete .aa-input, .algolia-autocomplete .aa-hint {
  width: 100%;
}

.algolia-autocomplete .aa-hint {
  color: #999;
}

.algolia-autocomplete .aa-dropdown-menu {
  width: 100%;
  background-color: #fff;
  border: 1px solid #999;
  border-top: none;
}

.algolia-autocomplete .aa-dropdown-menu .aa-suggestion {
  cursor: pointer;
  padding: 5px 4px;
}

.algolia-autocomplete .aa-dropdown-menu .aa-suggestion.aa-cursor {
  background-color: #B2D7FF;
}

.algolia-autocomplete .aa-dropdown-menu .aa-suggestion em {
  font-weight: bold;
  font-style: normal;
}
</style>
