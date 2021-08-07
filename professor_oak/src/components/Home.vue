<template>
  <div class="home_wrap">
      <div class="home_content container">
        <span class="debug">Home test</span>
        
        <!-- test blurr -->
        <div class="box">
          <span>Test blurr</span>
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
    background-image: url('../assets/images/home_bg.jpg');
    height: 100vh;
    background-position: center;
    background-repeat: no-repeat;
    background-size: initial;
}

.debug {
  color: var(--red);
}

.container {
  display: flex;
  width: 100%;
  height: 100%;

  align-items: center;
  justify-content: center;
}

.box {
  max-width: 50%;
  max-height: 50%;

  font-family: sans-serif;
  color: var(--white);


  background-color: rgba(196, 203, 208, .3);
  border-radius: 6px;
  text-align: center;
  line-height: 2;

  -webkit-backdrop-filter: blur(12px);
  backdrop-filter: blur(12px);

  padding: 22px 44px;
}
</style>