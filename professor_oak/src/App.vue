<template>
  <div id="app">
    <Home 
    :list="pokemon"
    :staticList="pokemon"
    :type="types"
    :indice="i"
    @clicked="pokemonGetter"
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
      i:0, //test numero pokedex
      url : 'https://pokeapi.co/api/v2/',
      // pokemonList : pokemon + 'pokemon?limit=898',
      pokemon : [],
      types: [],

    }
  },
  created() {
    console.log("created");
    console.log("pokemon : " , this.url);
    this.pokemonGetter(0);//axios call per lista pokemon
    this.typeGetter(); //axio call per lista tipi
  },
  methods: {
      test(value){
        console.log("emit test function",value);
      },
      pokemonGetter(interval){
        
        this.i=interval +1; //test numero pokedex (mi da il numero di partenza)
        // lista pokemon
        this.pokemon = ""; //i shit you not this was an entire afternoon of trial and error arasgjsdkjfsndkfjsnfkdjsnkjsnfkfjn
        console.log(this.url + 'pokemon?limit='+20+'&offset='+interval);
        if(interval >= 880){
          axios
            .get(this.url + 'pokemon?limit='+18+'&offset='+interval)
            .then(response =>{
              // console.log(response.data.results); //object {name , url}
              this.pokemon = response.data.results; //lista di tutti i pokemon
              
              console.log("pokemon list : " , this.pokemon);
            })
        }
        else{
          axios
            .get(this.url + 'pokemon?limit='+20+'&offset='+interval)
            .then(response =>{
              // console.log(response.data.results); //object {name , url}
              this.pokemon = response.data.results; //lista di tutti i pokemon

              console.log("pokemon list : " , this.pokemon);
            })
        }
       
      },
      typeGetter(){
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
