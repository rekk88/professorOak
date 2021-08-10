<template>
  <div class="sidebar_wrap py-2 px-3">
    <ul class="pokemon_list ps-0">
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li class="pokemon_list_item ps-2">#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
      <li>#10 ditto</li>
    </ul>
  </div>
</template>

<script>
export default {
name:'Sidebar'
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