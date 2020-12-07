<template>
  <div id="app">




    <div class="column is-half is-offset-one-quarter">
    <h1>Pokedex</h1>
    <input class="input is-rounded" type="text" placeholder="Buscar Pokemon" v-model="busca">
    <button @click="buscar()" class="button is-fullwidth buscaBtn is-success">Buscar</button>



      <div v-for="(poke, index) in filterPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>



  </div>
</template>

<script>

  import axios from 'axios';
  import Pokemon from './components/Pokemon';

  export default {
    name: 'App',
    components: {
      Pokemon
    },
    data(){
      return {
        pokemons: [],
        filterPokemons: [],
        busca: ''
      }
    },
    created: function(){
      
      axios.get("https://pokeapi.co/api/v2/pokemon? limit =20&offset=0").then(res => {
        this.pokemons = res.data.results;
        this.filterPokemons = res.data.results;
        //console.log(this.pokemons);
      })
    },
    methods: {
      buscar: function(){
        this.filterPokemons = this.pokemons;
        if(this.busca == '' || this.busca == ' '){
          this.filterPokemons = this.pokemons;
        } else {
          this.filterPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
        }
      }
    },
    computed: {
      /*
      resultadoBusca: function(){
        if(this.busca == '' || this.busca == ' '){
          return this.pokemons;
        } else {
          return this.pokemons.filter(pokemon => pokemon.name == this.busca)
        }
        */
      }



  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.buscaBtn{
  margin-top: 2%;
}
</style>
