<template>
 <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img id="logo" src="./assets/logo_fukuta.png"/>
      
      <p class="title is-2">Pokedexx</p>
      <p class="subtitle is-5">Consumindo API com NodeJS + Vue + Bulma + Axios + PokeAPI</p>
      <input class="input is-primary is-rounded" type="text" v-model="busca" placeholder="buscar pokemon pelo nome">
      <hr>
      <div v-for="(poke,index) in resultadoBusca" v-bind:key = "index">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"></Pokemon>
    </div>

  </div>
   
 </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      busca: ''
    }
  },
  created: function() {
   
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista dos pokemons");
      this.pokemons = res.data.results;
    })

  },
  components: {
    Pokemon
  },
  computed: {
    resultadoBusca: function() {
      if(this.busca == '' || this.busca == ' ') {
        return this.pokemons;
      } else {
        return this.pokemons.filter( pokemon => pokemon.name == this.busca)
      }
    }
  }
}
</script>

<style>
body {
  background-color: #f1f5f8;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#logo {
  width: 30%;
}

#buscaBtn {
  margin-top:2%;
}
</style>
