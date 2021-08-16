<template>
  <div class="container p-1">
    <div class="row">
      <div class="col-lg">
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

            <span class="navbar-text tag_line">Gotta catch 'em all!</span>


            <button 
              class="btn btn-outline-success" 
              role="button" 
              aria-expanded="false" 
              @click="pokemonRandomGet()">
                <i class="bi bi-arrow-repeat me-2"></i>
                  Surprise me
            </button>
          </div>
        </nav>
      </div>
    </div>

    <div class="text-center p-1">
      <div v-if="pokeSprite != ''" class="pokeFortunato my_nav p-0 m-0">
        <span class="navbar-text tag_line m-0 p-0">Sconfiggi la Lega solamente con: </span>
        <span v-for="(item, index) in pokemonListRandom" :key="index" class="text-capitalize m-0 p-0">
          <a :href="item.url" class="navbar-text text-decoration-none tag_line m-0 p-0">{{item.name}}</a>
        </span>
        <img :src="pokeSprite" alt="pokemon-fortunato" class="ms-0">
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

  props:["tipi", "lista"],
  
  data() {
    return {
    url: 'https://pokeapi.co/api/v2/',
    randomNumber: [],
    pokemonListRandom: [],
    pokeSprite:'',
  }
},

 created() {
  // this.pokemonRandomGet();
},

  methods: {
    
    pokemonRandomGet() { // Pesco 20 pokemon casuali
    this.randomNumber = Math.floor(Math.random() * (898 - 0 + 1) + 0);

      axios
        .get(this.url + 'pokemon?limit=898')
        
        .then(response => {
          this.pokemonListRandom = []
          console.log(this.randomNumber);
          this.pokemonListRandom.push(response.data.results[this.randomNumber -1]);
          console.log(this.pokemonListRandom);

        })

      axios
        .get(this.url + 'pokemon' + '/' + this.randomNumber)
        .then(response => {
          console.log(this.url + 'pokemon' + '/' + this.randomNumber);
          this.pokeSprite = response.data.sprites.front_default;
          console.log('MIO lOG',this.pokeSprite);
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

img {
  width: 85px;
}

.pokeFortunato {
  width: 35%;
  margin: 0 auto!important;
}
</style>