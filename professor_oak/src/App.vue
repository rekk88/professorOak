<template>
  <div id="app">
    <Home 
    :list="pokemon"
    :type="types"
  />
  </div>
</template>


<script>
import Home from './components/Home.vue'
import axios from 'axios'

export default {
  name: 'App',

  components: {
    Home,
  
  },
  data() {
    return {
      x : 0,
      url : 'https://pokeapi.co/api/v2/',
      // pokemonList : pokemon + 'pokemon?limit=898',
      pokemon : [],
      names : [],
      types: [],
    }
  },
  created() {
    console.log("created");
    console.log("pokemon : " , this.url);
    this.pokemonGetter(); //axios call per lista pokemon e lista tipi
  },
  methods: {
      pokemonGetter(){
        // lista pokemon
        axios
          .get(this.url + 'pokemon?limit=20')
          .then(response =>{
            console.log(response.data.results); //object {name , url}
            this.pokemon = response.data.results; //lista di tutti i pokemon
           
            console.log("pokemon list : " , this.pokemon);
          })

          
        // Type
        axios 
          .get(this.url + 'type')
          .then(response => {
            this.types = response.data.results;
            console.log("pokemon type: " , this.types);
          })
      }
  },  
}
</script>


<style lang="scss">
@import 'scss/commons.scss';
@import 'scss/colors.scss';
@import 'scss/type.scss';


#app {
  // font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
