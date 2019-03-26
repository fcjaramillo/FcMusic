<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>FcMusic</h1>
    <select name="" id="" v-model= "selectedCountry">
      <option v-for= "country in countries" :value= "country.value" :key= "country.value">
        {{ country.name }}
      </option>
    </select>
    <spinner v-show="cargando">

    </spinner>
    <ul>
      <artist v-for= "artist in artists" :artist= "artist" :key= "artist.mbid" >
      </artist>
      <!-- <li v-for= "artist in artists" :key= "artist.name"> {{ artist.name }} </li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li> -->
    </ul>
  </div>
</template>

<script>
import getArtists from './api'
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries: [
        { name : 'Colombia', value: 'colombia' },
        { name : 'Argentina', value: 'argentina' },
        { name : 'España', value: 'spain' }
      ],
      selectedCountry : 'colombia',
      cargando: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtist(){
      const _this = this
      this.artists = []
      this.cargando = true
      getArtists(this.selectedCountry)
        .then(function(artists){
          _this.artists = artists
          _this.cargando = false
        })
    }
  },
  mounted: function (){
    this.refreshArtist();
  },
  watch:{
    selectedCountry: function () {
      this.refreshArtist();
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
