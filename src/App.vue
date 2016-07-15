<template>
  <div id="app">
    <input id="search-input" type="text">
  </div>
</template>

<script>
let algoliasearch = require('algoliasearch')
let autocomplete = require('../vendor/autocomplete.min.js')

export default {
  data () {
    return {

    }
  },
  ready: () => {
    var client = algoliasearch('6DLEN782G1', '6ca42b1a471f2cc5def1aa1fedd10257')
    var index = client.initIndex('dev_knowledges')

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
