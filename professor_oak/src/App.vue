<template>
  <div id="app">
    <Home />
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
      pokemon : 'https://pokeapi.co/api/v2/',
      // pokemonList : pokemon + 'pokemon?limit=898',
      pokemonNames : [],
      names : [],
    }
  },
  created() {
    console.log("created");
    console.log("pokemon : " , this.pokemon);
    axios
      .get(this.pokemon + 'pokemon?limit=898')
      .then(response =>{
        console.log(response.data.results); //object {name , url}
        this.names = response.data.results;
        this.names.forEach(element => {
          this.pokemonNames.push(element.name);
          
        });
        console.log("pokemon list : " , this.pokemonNames);
      })
  },
  methods: {
      
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
