<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>App VueMusic</h1>
    <select v-model="selectedCountry">
      <option v-for="country in countries" v-bind:value="country.value"> {{ country.name }}</option>
    </select>
    <ul>
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid">
        {{ artist.name }}
      </artist>
    </ul>
  </div>
</template>

<script>
import Artist from './components/Artist.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
      { name: 'Argentina', value: 'argentina' },
      { name: 'Colombia', value: 'colombia' },
      { name: 'España', value: 'spain' },
      { name: 'Venezuela', value: 'venezuela' },
      ],
      selectedCountry: 'venezuela'
    }
  },
  components: {
    Artist: Artist
  },
  methods: {
    refreshArtist(){
      const self = this
      getArtists(this.selectedCountry)
        .then(function (artist){
          self.artists = artist
        })
    }
  },
  mounted(){
    this.refreshArtist()
  },
  watch: {
    selectedCountry(){
    this.refreshArtist()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
