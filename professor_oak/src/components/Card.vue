<template>
  <div class="card poke_card flip_card container border-0" style="width: 18rem;">
    <div class="flip_inner">
      <div class="flip_front">
        <img :src="sprite" class="card-img-top rounded-circle" alt="sprite">
      </div>
      <div class="flip_back rounded-circle">
        <!-- back text -->
        <img :src="official_artwork" class="card-img-top rounded-circle" alt="back image">
        <div class="card_back_text">{{descriptionText}}</div>
      </div>
    </div>
    
    <div class="card-body">
      <h5 class="card-title">
        <!-- pokemon id and name here -->
        <!-- <span class="pokemon_number">#20</span> <span class="pokemon_name">{{n}}</span> -->
        <span class="pokemon_number">#{{numberPokedex}}</span> <span class="pokemon_name text-capitalize"><a :href="urlPokemon" class="text-decoration-none">{{n}}</a></span>
      </h5>
      
      <!-- type here -->
      <h6 class="d-flex">
        <!-- first -->
        <span class="pokemon_type flying me-1">{{type1.name}}</span> 
        <!-- second -->
        <span class=" pokemon_type dragon ms-1">Dragon</span>
      </h6>

      <!-- <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
      <a href="#" class="btn btn-primary">Go somewhere</a> -->
    </div>
  </div>
</template>


<script>
import axios from 'axios'
export default {
 name: 'Card',
 components:{},
 data() {
   return {
     test : this.n,
     sprite : "",
     descriptionText:"",
     official_artwork : "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+this.numberPokedex+".png",
     descriptionUrl : "https://pokeapi.co/api/v2/pokemon-species/"+this.numberPokedex+"/"
   }
 },
//  props:{
//    nome : String,
//    urlPokemon : String
//  }
props:["n", "urlPokemon", "numberPokedex"],
mounted() {
  console.log(this.urlPokemon)
  // axios
  //   .get(this.urlPokemon)
  //   .then(response =>{
  //     // console.log(response.data.sprites.other.official-artwork);
  //     console.log(this.official_artwork);
  //     this.sprite = response.data.sprites.front_default;

  //   })
  axios.all([
    axios.get(this.urlPokemon), //chiamata per sprite del singolo pokemon
    axios.get(this.descriptionUrl) //chiamata per la descrizione del pokemon
  ])
  .then(axios.spread((obj1, obj2)=>{
    console.log("obj 1 : ",obj1.data.sprites.front_default);
    //flavor_text_entries[x] x -> indica la versione del testo che andiamo a selezionare
    console.log("obj 2 : ",obj2.data.flavor_text_entries[0].flavor_text);
    this.sprite = obj1.data.sprites.front_default;
    this.descriptionText = obj2.data.flavor_text_entries[0].flavor_text;
  }));
},
}
</script>


<style lang="scss" scoped>
.poke_card {
  text-align: center;
  line-height: 2;   // ! Rivedere!!! 2px???
  color: var(--white);
  background-color: transparent;

  .card-img-top {
    // background-color: var(--grey-card);
    background-color: var(--dark-grey);
    backdrop-filter: blur(5px);

    border: 1px solid var(--transparent-grey);
    border-radius: 6px;
    box-shadow: -1px 1px 5px 9px var(--ultra-transparent-grey);
    padding: 15px;
  }

  .card-body {
    .card-title{
      font-weight: 600;
      
      .pokemon_number{
        color: var(--grey);
      }
    }
  }

  padding: 0px 44px;
}
</style>