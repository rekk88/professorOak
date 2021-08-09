<template>
  <div class="home_wrap">
    <div class="home_content container">
      <div class="text-center debug">Home test</div>
        
      <!-- test blurr -->
      <div class="poke_card mt-5">
        <div class="me-5">Diglett</div>
        <div class="container_image me-5">
          <img src="../assets/images/38.png" alt="poke" class="">
        </div>
        <div class="text-start">Se Diglett attraversa un terreno nel corso dei suoi scavi, lo lascia perfettamente lavorato e pronto per la semina.</div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
    name:'Home',
}
</script>


<style lang="scss" scoped>
.home_wrap {
  height: 100vh;
  background-image: url('../assets/images/home_bg2.jpg');
  background-size: initial;
  background-position: cover;
  background-repeat: no-repeat;
}

.debug {
  color: var(--red);
}

.poke_card {
  display: flex;
  width: 50%;
  height: 30%;

  align-items: start;
  justify-content: start;

  font-family: sans-serif;
  text-align: center;
  line-height: 2;
  color: var(--white);

  background-color: var(--transparent-grey);
  backdrop-filter: blur(5px);

  border: 1px solid var(--transparent-grey);
  border-radius: 6px;
  box-shadow: -1px 1px 5px 9px var(--ultra-transparent-grey);
  

  padding: 22px 44px;

  .container_image {
    width: 150px;
    height: 150px;
    object-fit: contain;
    
    img {
      width: 100%;
    }
  }
}
</style>