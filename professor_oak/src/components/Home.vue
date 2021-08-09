<template>
  <div class="home_wrap">
    <div class="home_content container">
      <div class="text-center debug">Home test</div>
        
      <!-- test blurr -->
      <Card />
    </div>
  </div>
</template>


<script>
import Card from './Card.vue'

export default {
    name:'Home',
    components :{
      Card
    }
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


</style>