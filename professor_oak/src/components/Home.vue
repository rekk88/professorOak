<template>
  <div class="home_wrap pb-4 overflow scrollbar">
    <div class="home_content">
      <div class="header_wrap"> 
        <Logo />
        <Header />
      </div>
        
      <!-- test blurr -->
      <div class="main_content_wrap container d-flex p-0 rounded mt-5">
         <div class="col overflow scrollbar">
            <div class="">
              <div class="p-0 ">
                <Sidebar />
              </div>
            </div>
        </div>
      <div class="container d-flex justify-content-center align-items-start col-10 py-3 overflow scrollbar">
       
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
import Logo from './Logo.vue'
import Header from './Header.vue'
import Sidebar from './Sidebar.vue'

export default {
  name: 'Home',

  components: {
    Logo,
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

  .home_content {
    height: 100%;

    .header_wrap {
      height: 20%;
    }

    .main_content_wrap {
      height: 80%;
      box-shadow: -1px 1px 5px 9px var(--ultra-transparent-grey);

      .card_wrap {
        height: max-content;
      }
    }
  }
}
</style>