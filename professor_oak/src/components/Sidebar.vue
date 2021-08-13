<template>
  <div class="sidebar_wrap h_100 py-2 px-3">
    <div class="pokemon_list_search input-group">
        <input type="text" class="form-control rounded-pill" placeholder="scrivi roba" aria-label="Search" v-model="ricerca">
    </div>
    <ul class="pokemon_list ps-0 pt-2 overflow scrollbar">
      <li class="pokemon_list_item ps-2" v-for="(item,i) in lista" :key="i">
        <span v-if="item.name.includes(ricerca)">
          <span class="pokemon_list_number">#{{i+1}} </span><span @click="visualizza(item.url)"><a href="#" class="pokemon_list_name">{{item.name}}</a></span>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
name:'Sidebar',
components:{

},
props:["lista"], //prop in arrivo da Home
data() {
  return {
    ricerca : "",
    k : this.pokemon,  
    filteredList : []
  }
},
mounted() {
  console.log(this.lista);
},
// computed:{
//   functionRicerca(){
//     console.log("input text aggiornato");
//     return "updated";
//   }
// },
updated() {
  console.log("input text aggiornato : " , this.ricerca) //test log
  console.log(this.lista);
},
methods: {
  visualizza(url2){ //da implementare prima la pagina del singolo pokemon
    console.log("url singolo pokemon" , url2); 
  }
},
}
</script>

<style lang="scss" scoped>
.sidebar_wrap {
  .pokemon_list_search{
    height: 5%;
  }
  .pokemon_list {
    height: 95%;
    list-style: none;
    font-weight: 600;
    
    li {    // selettore con tag li da eliminare
      width: 100%;
      line-height: 1.6;
    }
    
    .pokemon_list_item {
      text-shadow: -1px 1px var(--ultra-transparent-grey);
      .pokemon_list_name{
        text-decoration: none;
      }
    }
    
    .pokemon_list_item:hover {
      background-color: var(--ultra-transparent-grey);
      border-radius: 50rem !important;
    }
  }
}
</style>