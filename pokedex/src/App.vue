<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter"> 
      <h4 class="is-size-2"> Pokedex </h4>
      <input type="text" placeholder="Buscar pokemon" class="input is-rounded" v-model="busca">
      <button  class="button is-success is-fullwidth" id="buscaBtn" @click="buscar"> Buscar </button>
      <div v-for="(poke, index) in filterPoke" :key="index">
          <Pokemon :num="index" :name="poke.name" :url="poke.url"/>
      </div>
    </div>   
  </div>
</template>

<script>
import axios from "axios"
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      filterPoke: [],
      busca: ""
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(res => {
      console.log("Pegou as listas")
      this.pokemons = res.data.results
      this.filterPoke = res.data.results
    })

  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function() {
      this.filterPoke = this.pokemons
      if(this.busca == "" || this.busca == " ")
      {
         this.filterPoke = this.pokemons
      } else {
         this.filterPoke = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#buscaBtn {
  margin-top:10px;
}
</style>
