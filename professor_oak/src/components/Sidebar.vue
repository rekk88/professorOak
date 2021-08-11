<template>
  <div class="sidebar_wrap py-2 px-3">
    <ul class="pokemon_list ps-0">
      <li class="pokemon_list_item ps-2" v-for="(item,index) in lista" :key="index">
        <span>#{{index}} </span><span @click="visualizza(item.url)"><a href="#" >{{item.name}}</a></span>
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
    k : this.pokemon,  
  }
},
mounted() {
  console.log(this.lista);
},
methods: {
  visualizza(url2){
    console.log("url singolo pokemon" , url2);
  }
},
}
</script>

<style lang="scss" scoped>
.sidebar_wrap {
  .pokemon_list {
    list-style: none;
    font-weight: 600;
    
    li {    // selettore con tag li da eliminare
      width: 100%;
      line-height: 1.6;
    }
    
    .pokemon_list_item {
      text-shadow: -1px 1px var(--ultra-transparent-grey);
    }
    
    .pokemon_list_item:hover {
      background-color: var(--ultra-transparent-grey);
      border-radius: 50rem !important;
    }
  }
}
</style>