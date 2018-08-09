<template>
  <div id="app">
    <h3>Example 2</h3>
    <div>
      Data: {{ example1 }}
    </div>
    <button @click="getLanguage">Get Language</button>
    <button @click="getChampions">Get Championz</button>
    <hr> 
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'app',
  data () {
    return {
      example1: ''
    }
  },
  methods: {
    async getLanguage () {
      try {
        const res = await axios.post(
          'http://localhost:4000/graphql', {
          query: '{ language }'
        })
        this.example1 = res.data.data.language
        // eslint-disable-next-line
        console.log(res.data)
      } catch (e) {
        // eslint-disable-next-line
        console.log('err', e)
      }
    },
    async getChampions () {
      try {
        const res = await axios.post(
          'http://localhost:4000/graphql', {
          query: '{ getChampions { name } }'
        })
        this.example1 = res.data.data.getChampions
      } catch (e) {
        // eslint-disable-next-line
        console.log('err', e)
      }
    }

  }
}
</script>