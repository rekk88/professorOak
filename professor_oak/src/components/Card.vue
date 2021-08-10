<template>
 
<div class="card poke_card container border-0" style="width: 18rem;">
  <img src="../assets/images/38.png" class="card-img-top rounded-circle" alt="sprite">
  <div class="card-body">
    <h5 class="card-title">
        <!-- pokemon id and name here -->
        <span class="pokemon_number">#20</span> <span class="pokemon_name">Fox</span>
        <span class="pokemon_type fire">Fire</span>
        
    </h5>
    <!-- <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a> -->
  </div>
</div>
</template>

<script>
export default {
 name: 'Card',
}
</script>

<style lang="scss" scoped>
.poke_card {
  text-align: center;
  line-height: 2;
  color: var(--white);
  background-color: transparent;

  .card-img-top{
    background-color: var(--transparent-grey);
    backdrop-filter: blur(5px);

    border: 1px solid var(--transparent-grey);
    border-radius: 6px;
    box-shadow: -1px 1px 5px 9px var(--ultra-transparent-grey);
    padding: 15px;
  }
  .card-body{
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