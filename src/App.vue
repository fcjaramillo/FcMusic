<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>FcMusic</h1>
    <ul>
      <li v-for= "artist in artists" :key= "artist.name"> {{ artist.name }} </li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
  </div>
</template>

<script>
import getArtist from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[]
    }
  },
  mounted: function (){
    const _this = this
    getArtist()
      .then(function(artists){
        _this.artists = artists
      })
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
