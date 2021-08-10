<template>
  <div class="container text-center p-2">
    <img src="../assets/images/pokemon_logo.png" alt="logo" class="me-1">
    <img src="../assets/images/pokemon_team.png" alt="team" class="ms-2">
  </div>
</template>


<script>
export default {
    name:'Logo',
}
</script>


<style lang="scss" scoped>
img:first-child {
  height: 70px;
}

img:nth-child(2) {
  width: 200px;
}
</style>