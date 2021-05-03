<template>
  <div id="app">

    <img src= "./assets/pokeaqui.png">
    <h4 class="is-size-1"> Pokedex </h4>

    <div class="column is-half is-offset-one-quarter"> 

      <table class="table" align="center">
        <tr>
          <td height=70>
            <input type="text" placeholder="Type and click to find Pokemon" v-model="busca" class="input is-info"> 
          </td>
          <td>
            <button class="button is-primary" id="buscaBtn" @click="buscar">Search</button>
          </td>
        </tr>
      </table>

      <!-- <div v-for="(poke,index) in resultadoBusca"  :key="index">
      <div v-for="(poke,index) in pokemons"  :key="index"> 
      <div v-for="(poke,index) in filteredPokemons"  :key="index"> -->
      <div v-for="(poke,index) in filteredPokemons"  :key="poke.url">
        <!--
          <h1>{{index+1}} {{poke.name}}</h1>
        -->
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
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function() {
    //console.log(axios);
    //console.log('teste');
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then( res => {
      //console.log(res.data.results);
      console.log('Pegando a lista de pokemons');
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
      //console.log('this.pokemons');
    });
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function() {
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.substring(0,(this.busca.length)) == this.busca);
      }
    }
  },
  computed: {
    /*
    resultadoBusca: function() {
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name.substring(0,(this.busca.length)) == this.busca);
      }
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
  margin-top: 60px;
}
</style>
