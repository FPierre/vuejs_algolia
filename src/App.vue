<template>
  <div id="app">
    <input id="search-box" type="text">

    <div id="tags"></div>
    <div id="hits-container"></div>
    <div id="pagination-container"></div>
  </div>
</template>

<script>
let instantsearch = require('instantsearch.js')

export default {
  data () {
    return {

    }
  },
  ready: () => {
    let search = instantsearch({
      appId: '6DLEN782G1',
      apiKey: '6ca42b1a471f2cc5def1aa1fedd10257',
      indexName: 'dev_knowledges'
    })

    search.addWidget(
      instantsearch.widgets.searchBox({
        container: '#search-box',
        placeholder: 'Search for knowledges',
        poweredBy: true
      })
    )

    search.addWidget(
      instantsearch.widgets.hits({
        container: '#hits-container',
        hitsPerPage: 10,
        templates: {
          item: 'Knowledge {{ objectID }}'
        }
      })
    )

    search.addWidget(
      instantsearch.widgets.pagination({
        container: '#pagination-container',
        maxPages: 20
      })
    )

    search.addWidget(
      instantsearch.widgets.refinementList({
        container: '#tags',
        attributeName: 'tags'
      })
    )

    search.start()
  }
}
</script>

<style>

</style>
