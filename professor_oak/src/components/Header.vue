<template>
  <div class="container p-1">
    <div class="row">
      <div class="col-lg-6">
        <nav class="my_nav navbar">
          <div class="container-fluid">
            <form class="d-flex">
              <input class="form-control me-2 opacity-75" type="search" placeholder="Search a Pokémon" aria-label="Search">
              <button class="btn btn-outline-success" type="submit">
                <i class="bi bi-search"></i>
              </button>
            </form>

            <li class="nav nav-item dropdown position-relative">
              <a class="nav-link link-success dropdown-toggle" 
                 data-bs-toggle="dropdown" 
                 href="#" role="button" 
                 aria-expanded="false">
                  Filter by type
              </a>
                  
              <ul class="dropdown-menu position-absolute mt-3 p-1 my_drpo-menu_color">
                <li v-for="(item, index) in tipi" :key="index" :class="item.name">
                  <a class="dropdown-item" href="#">{{item.name}}</a>
                </li> 
              </ul>
            </li>
          </div>
        </nav>
      </div>

      <div class="col-lg-6">
        <nav class="my_nav navbar navbar-nav navbar-collapse">
          <div class="container-fluid">
            <span class="navbar-text tag_line">Gotta catch 'em all!</span>

            <span class="btn btn-outline-success">
              <i class="bi bi-arrow-repeat me-2"></i>
              Surprise me
            </span>
          </div>
        </nav>
        <!-- pesco 20 pokemon a caso -->
        <span v-for="(item, index) in pokemonListRandom" :key="index">{{item.name}} </span>
      </div>
    </div>
  </div>
</template>


<script>


import axios from 'axios'
export default {
  name:'Header',

  components: {
    
  },

  props:["tipi"],
  
  data() {
    return {
    url: 'https://pokeapi.co/api/v2/',
    randomNumber: [],
    pokemonListRandom: [],

  }
},

 created() {
  this.pokemonRandomGet();
},

  methods: {
    pokemonRandomGet() { // Pesco 20 pokemon casuali
      axios
        .get(this.url + 'pokemon?limit=898') 

        .then(response => {
          for (var i = 0; i < 20; i++) {
            this.randomNumber = Math.floor(Math.random() * (898 - 0 + 1) + 0); // genero un numero casuale che farà da indice per pescare il poke
            console.log(this.randomNumber);
            this.pokemonListRandom.push(response.data.results[this.randomNumber - 1]); // pusho il poke nell'array (-1 per il numero di pokedex)
            console.log(this.pokemonListRandom);
          }
        })
    }
  }
}
</script>


<style lang="scss" scoped>
.my_nav {
  background-color: var(--transparent-grey);

  border: 1px solid var(--transparent-grey);
  border-radius: 6px;
}

.my_drpo-menu_color {
  background-color: var(--ultra-transparent-grey);
  backdrop-filter: blur(5px);
}

.dropdown-item:hover {
  background-color: var(--transparent-grey);
  border-radius: 50rem!important;
}

input:focus { 
  border-color: var(--greenBulba);
  box-shadow: 1px 1px 5px var(--greenBulba);
}

.tag_line {
  color: var(--greenBulba);
}
</style>