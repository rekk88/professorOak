<template>
  <div class="home_wrap pb-4">
    <div class="home_content">
      <div class="header_wrap">
        <Logo/>
        <Header 
          :tipi="type"
        />

      </div>
        
      <!-- test blurr -->
      <div class="container text-center">
         <div class="row">
          <div class="col d-inline" v-for="(button,index) in buttons" :key="index" @click="page([0,20])">
            <div class="d-inline" v-if="index < 44"> 
              <div  @click="page(button)">
               {{button}}-{{button + 20}}

              </div>
            </div>
          </div>
          <div class="col" @click="page(20)">
            20-40
          </div>
        </div>
      </div>
      
      <div class="main_content_wrap container d-flex p-0 rounded">
         <div class="col">
            <div class="h_100">
              <div class="p-0 h_100">
                <Sidebar :lista="list" :n="indice"/>
              </div>
            </div>
        </div>
        
      <div class="container d-flex justify-content-center align-items-start col-10 py-3 overflow scrollbar">
       
        <div class="row row-cols-3">
          <div class="col card_wrap" v-for="(item, index) in list" :key="index"> 
            <div> <!--v-if per la ricerca da header -->
              <Card :n="item.name" 
                    :urlPokemon="item.url" 
                    :numberPokedex="index + indice"
                    ref="Card"
              /> 
            </div>
          </div>
        </div>
        
      </div>
      </div>
     
    </div>
  </div>
</template>


<script>
import Card from './Card.vue'
import Header from './Header.vue'
import Logo from './Logo.vue'
import Sidebar from './Sidebar.vue'

export default {
    name: 'Home',
    
    components: {
      Logo,
      Header,
      Card,
      Sidebar
    },
    //prop in arrivo da App (con il risultato della chiamata axios)
    props:["list", "type","indice"], //list : lista pokemon ; type : lista tipi 
    data() {
      return {
        buttons : [],
      }
    },
    methods: {
      page(vet){
        console.log("emit value : " , vet);
        this.$emit('clicked',vet); //vet -> emit -> interval
        for(let i=vet ; i <= (vet+20) ; i++){
          console.log("indice i di vet : ", i);
          this.$refs.Card[i].img_type_Getter();
        }
      }
    },
   
    created() {
      // console.log(this.list);
      for(let i=0 ; i <=880 ; i=i+20){
        this.buttons.push(i);
      }
      console.log(this.buttons);
    },
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
      height: 30%;
    }
    .main_content_wrap{
      height: 65%;
      box-shadow: -1px 1px 5px 9px var(--ultra-transparent-grey);
      .card_wrap{
        height: max-content;

      }
    }
  }
}
</style>