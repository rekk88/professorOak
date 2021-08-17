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
        <span class="pokemon_number" @click="refsRead">#{{numberPokedex}}</span> <span class="pokemon_name text-capitalize"><a :href="urlPokemon" class="text-decoration-none">{{n}}</a></span>
      </h5>
      
      <!-- type here -->
      <h6 class="text-center">
        <!-- first -->
        <span :class="type1.name">{{type1.name}}</span> 
        <!-- second -->
        <span :class="type2.name">{{type2.name}}</span>
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
     descriptionUrl : "https://pokeapi.co/api/v2/pokemon-species/"+this.numberPokedex+"/",
     type1: "",
     type2: "",
   }
 },

props:["n", "urlPokemon", "numberPokedex"],
methods: {
  refsRead(){
    console.log(this.$refs);
  },
  test2: function(){
    console.log("sono il metodo test2!");
  },
 
  img_type_Getter(){
    this.sprite="";
    this.descriptionText="";
    this.official_artwork = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+this.numberPokedex+".png",
    this.descriptionUrl="https://pokeapi.co/api/v2/pokemon-species/"+this.numberPokedex+"/",


    axios.all([
      axios.get(this.urlPokemon), //chiamata per sprite e tipo del singolo pokemon
      axios.get(this.descriptionUrl) //chiamata per la descrizione del pokemon
    ])
    .then(axios.spread((obj1, obj2)=>{
    // console.log("obj 1 : ",obj1.data.sprites.front_default);
   
    this.sprite = obj1.data.sprites.front_default;
    obj2.data.flavor_text_entries.forEach(element => {
      // console.log("flavor text : ",element);
      if(element.language.name == "en"){
        this.descriptionText = element.flavor_text;
      }
    });
    // this.descriptionText = obj2.data.flavor_text_entries[0].flavor_text;
   
    this.type1 = obj1.data.types[0].type;
      if (obj1.data.types.length == 2) {
        this.type2 = obj1.data.types[1].type;
      }
      else this.type2 = '';
  }));
  },

 
},
mounted() {
  // console.log(this.urlPokemon),
  this.img_type_Getter()
},

}
</script>


<style lang="scss" scoped>
.poke_card {
  text-align: center;
  line-height: 1.3rem;
  color: var(--white);
  background-color: transparent;

  .card-img-top {
    // background-color: var(--grey-card);
    background-color: var(--dark-grey);
    backdrop-filter: blur(5px);

    border: 1px solid var(--ultra-transparent-grey);
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

  padding: 0px 55px;
}
</style>