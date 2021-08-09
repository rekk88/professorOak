<template>
  <div class="home_wrap">
    <div class="home_content">
      <div class="header_wrap"> 
        <Header />

      </div>
        
      <!-- test blurr -->
      <div class="main_content_wrap container d-flex">
         <div class="col debug2">
            <div class="row row-col">
              <div class="col">
                <Sidebar />
              </div>
            </div>
        </div>
      <div class="container d-flex justify-content-center align-items-start col-9 py-3 overflow-auto debug2">
       
        <div class="row row-cols-3">
          <div class="col card_wrap"> <Card /> </div>
          <div class="col card_wrap"> <Card /> </div>
          <div class="col card_wrap"> <Card /> </div>

          <div class="col card_wrap"> <Card /> </div>
          <div class="col card_wrap"> <Card /> </div>
          <div class="col card_wrap"> <Card /> </div>
          

          <div class="col card_wrap"> <Card /> </div>
          <div class="col card_wrap"> <Card /> </div>
          <div class="col card_wrap"> <Card /> </div>
        </div>
        
      </div>
      </div>
     
    </div>
  </div>
</template>


<script>
import Card from './Card.vue'
import Header from './Header.vue'
import Sidebar from './Sidebar.vue'
export default {
    name: 'Home',

    components: {
      Header,
      Card,
      Sidebar
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
  .home_content{
    height: 100%;
    .header_wrap{
      height: 20%;
    }
    .main_content_wrap{
      height: 80%;

      .card_wrap{
        height: max-content;

      }
    }
  }
  
}
</style>