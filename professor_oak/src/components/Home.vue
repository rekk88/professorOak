<template>
  <div class="home_wrap">
    <div class="home_content container">
      <Header />
        
      <!-- test blurr -->
      <Card />
    </div>
  </div>
</template>


<script>
import Card from './Card.vue'
import Header from './Header.vue'

export default {
    name: 'Home',

    components: {
      Header,
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