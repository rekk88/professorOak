<template>
  <div id="creator_box">
    <div class="made_by text-center text-white fs-6">
      Made with 
      <span class="fs-5 fw-bold heart">&#10084; </span> 
      by
    </div>

    <div class="container mt-2 d-flex justify-content-center text-white">
      <div class="creators d-flex">
        <div>
          <a 
            href="https://www.linkedin.com/in/carmelo-granvillano/" 
            target="_blank" 
            class="d-block text-center">
              <img  
                src="../assets/images/carmelo.jpg" 
                alt="Carmelo Granvillano">
          </a>
          <div class="text-center">megralo</div>
        </div>

        <div class="ms-3">
          <a 
            href="https://www.linkedin.com/in/maicolmatteoli/" 
            target="_blank" 
            class="d-block text-center">
              <img  
                src="../assets/images/maicol.jpg" 
                alt="Maicol Matteoli">
          </a>
          <div class="text-center">rakaro</div>
        </div> 
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: 'Footer'
}
</script>


<style scoped lang="scss">
#creator_box {
  position: absolute;
  bottom: 80px;
  left: 40%;
  transform: translate(50%, 50%);

  img {
    width: 60px;
    border-radius: 50%;
  }

  .heart {
    color: tomato;
  }
}

</style>
