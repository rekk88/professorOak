<template>
  <div class="home_wrap">
      <div class="home_content container">
        <span class="debug">Home test</span>
      </div>
  </div>
</template>


<script>
export default {
    name:'Home',
}
</script>


<style lang="scss" scoped>
.home_wrap{
    background-image: url('../assets/images/home_bg.jpg');
    height: 100vh;
    background-repeat: no-repeat;
}

.debug {
  color: var(--red);
}
</style>