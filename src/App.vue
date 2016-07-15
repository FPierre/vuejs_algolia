<template>
  <div id="app">
    <input id="search-input" type="text">

    <div id="hits-container"></div>
  </div>
</template>

<script>
let algoliasearch = require('algoliasearch')

export default {
  data () {
    return {

    }
  },
  ready: () => {
    let client = algoliasearch('6DLEN782G1', '6ca42b1a471f2cc5def1aa1fedd10257')
    let index = client.initIndex('dev_knowledges')

    index.search('git', function searchDone(err, content) {
      console.log(err, content)
    })

    index.search('ruby')
      .then(function searchSuccess(content) {
        console.log(content)
      })
      .catch(function searchFailure(err) {
        console.error(err)
      })
  }
}
</script>

<style>

</style>
