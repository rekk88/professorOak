<template>
  <div class="card poke_card flip_card container border-0" style="width: 18rem;">
    <div class="flip_inner">
      <div class="flip_front">
        <img src="../assets/images/38.png" class="card-img-top rounded-circle" alt="sprite">
      </div>
      <div class="flip_back rounded-circle">
        <!-- back text -->
        <img src="../assets/images/5.png" class="card-img-top rounded-circle" alt="back image">
        <div class="card_back_text">some back text , some more text</div>
      </div>
    </div>
    
    <div class="card-body">
      <h5 class="card-title">
        <!-- pokemon id and name here -->
        <span class="pokemon_number">#20</span> <span class="pokemon_name">{{n}}{{urlPokemon}}</span>
      </h5>
      
      <!-- type here -->
      <h6 class="d-flex">
        <!-- first -->
        <span class="pokemon_type flying me-1">Flying</span> 
        <!-- second -->
        <span class=" pokemon_type dragon ms-1">Dragon</span>
      </h6>

      <!-- <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
      <a href="#" class="btn btn-primary">Go somewhere</a> -->
    </div>
  </div>
</template>


<script>
export default {
 name: 'Card',
 components:{},
//  props:{
//    nome : String,
//    urlPokemon : String
//  }
props:["n","urlPokemon"],
mounted() {
  console.log(this.urlPokemon)
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