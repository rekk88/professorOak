<template>
  <div class="card poke_card flip_card container border-0" style="width: 18rem;" :key="vai" @load="img_type_getter()">
    <div class="flip_inner">
      <div class="flip_front">
        <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+this.readId()+'.png'" class="card-img-top rounded-circle" alt="sprite">
      </div>
      <div class="flip_back rounded-circle">
        <!-- back text -->
        <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/'+this.readId()+'.png'" class="card-img-top rounded-circle" alt="back image">
        <div class="card_back_text" :key="descrizione">{{descriptionText}}</div>
      </div>
    </div>

    <div class="card-body">
      <h5 class="card-title">
        <!-- pokemon id and name here -->
        <span class="pokemon_number" @click="refsRead">#{{readId()}}</span> <span class="pokemon_name text-capitalize"><a :href="pokemon.url" class="text-decoration-none">{{pokemon.name}}</a></span>
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
     official_artwork : "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+this.readId()+".png",
     descriptionUrl: "https://pokeapi.co/api/v2/pokemon-species/"+this.pokemon.pokemonID+"/",
     testP: this.p,
     type1: "",
     type2: "",
     id: this.pokemon.pokemonID,
    //  show:false,
     vai:0,
     descrizione:0,
     n:0
   }
 },

props:["pokemon","p"],
methods: {
  refsRead(){
    console.log(this.$refs);
  },
  test2: function(){
    console.log("sono il metodo test2!");
  },
  readId:function()
  {
      const id_split = this.pokemon.url.split('/')
      let id = id_split.pop()
      id = id_split.pop()

      return id
  },
  async img_type_Getter()
  {
    this.sprite="";
    this.descriptionText=" ";
    this.official_artwork = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+this.id+".png",
    this.descriptionUrl="https://pokeapi.co/api/v2/pokemon-species/"+this.pokemon.pokemonID+"/",
    // let response2 = await axios.get(this.pokemon.url);
    // this.type1 = response2.data.types[0].type;
    // if (response2.data.types.length == 2) {
    //   this.type2 = response2.data.types[1].type;
    // }
    // else this.type2 = '';
    axios.all([
      axios.get(this.pokemon.url), //chiamata per sprite e tipo del singolo pokemon
    ])
    .then(axios.spread((obj1)=>{
    // console.log("obj 1 : ",obj1.data.sprites.front_default);
    console.log("obj 1 :",obj1.data.types[0].type);
    // console.log(obj1.data.id);
    this.descriptionUrl="https://pokeapi.co/api/v2/pokemon-species/"+obj1.data.id+"/";

      axios.get(this.descriptionUrl)
        .then(response =>{
          // console.log(response.data.flavor_text_entries);
          response.data.flavor_text_entries.forEach(element =>{
            if (element.language.name == "en") {
              this.descriptionText = element.flavor_text;
              // console.log(this.descriptionText);
            }
          })
        })
    // console.log(response2.data);
    this.sprite = obj1.data.sprites.front_default;
    

    this.type1 = obj1.data.types[0].type;
    if (obj1.data.types.length == 2) {
      this.type2 = obj1.data.types[1].type;
    }
    else this.type2 = '';
    // console.log(this.type1.name);
    this.descrizione++;
    this.vai++;
    this.testP=false;
    setTimeout(() => {
      this.testP=true;
    }, 500);
  }));

  },


},
mounted() {

},

created() {
 this.img_type_Getter();
//  console.log("created");
  this.n=0;
},
updated() {
  this.id = this.pokemon.pokemonID;
  this.descriptionUrl = "https://pokeapi.co/api/v2/pokemon-species/"+this.pokemon.pokemonID+"/";

  if(this.n < 1){
     axios.get(this.descriptionUrl)
        .then(response =>{
          // console.log(response.data.flavor_text_entries);
          response.data.flavor_text_entries.forEach(element =>{
            if (element.language.name == "en") {
              this.descriptionText = element.flavor_text;
              // console.log(this.descriptionText);
            }
          })
        })
    this.n++;
  }

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