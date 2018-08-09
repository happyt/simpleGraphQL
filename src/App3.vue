<template>
  <div id="app">
    <h3>Example 3</h3>
    <div>
      Data: {{ results }}
    </div>
    <button @click="getLanguage">Get Language</button>
    <button @click="getChampions">Get Champions</button>
    <button @click="getChampionByName">Get Champion</button>
    <hr> 
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'app',
  data () {
    return {
      results: ''
    }
  },
  methods: {
    async getLanguage () {
      try {
        const res = await axios.post(
          'http://localhost:4000/graphql', {
          query: '{ language }'
        })
        this.results = res.data.data.language
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
        this.results = res.data.data.getChampion
        // eslint-disable-next-line
        console.log(res.data)
      } catch (e) {
        // eslint-disable-next-line
        console.log('err', e)
      }
    },
    async getChampionByName () {
      const res = await axios.post('http://localhost:4000/graphql', {
        query: `
          query getChampionByName($championName: String!) {
            getChampionByName(name: $championName) {
              name
              attackDamage
            }
          }`,
          variables: {
            championName: 'Ashe'
          }
      })
      // eslint-disable-next-line
      console.log(res.data)
      this.results = res.data.data.getChampionByName
      
    }

  }
}
</script>