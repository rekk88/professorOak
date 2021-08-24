<template>
  <div class="home_wrap pb-4">
    <div class="home_content">
      <div class="header_wrap">
        <Logo/>
        <Header 
          :tipi="type"
          @searchForm="searchPokemon"
        />
      </div>
        
      <div class="container text-center mb-3 button_container_wrap">
        <div class="button_container">
          <div class="d-inline-block" v-for="(button,index) in buttons" :key="index">
            <div v-if="index < 44"> 
              <div class="test_button"  @click="page(button)">
                {{button}}-{{button + 20}}
              </div>
             
            </div>
            <div class="test_button" v-else @click="page(880)">
              881-898
            </div>
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
          <div v-if="filteredList.length == 0">
            <div class="row row-cols-3">
                <div class="col card_wrap" v-for="(item, index) in list" :key="index"> 
                  <div class=""> <!--v-if per la ricerca da header -->
                      <Card :n="item.name" 
                          :urlPokemon="item.url" 
                          :numberPokedex="index + indice"
                          :search="searchP" 
                          ref="Card"                    
                      /> 
                  </div>  
                </div>
            </div>
          </div>
          <div v-else>
             <div class="row row-cols-3">
                <div class="col card_wrap" v-for="(item, index) in filteredList" :key="index"> 
                  <div class=""> <!--v-if per la ricerca da header -->
                      <Card :n="item.nome" 
                          :urlPokemon="item.url" 
                          :numberPokedex="item.id"
                          ref="Card"                    
                      /> 
                  </div>  
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios'
// import axios from 'axios'
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
    props:["list", "type", "indice"], //list : lista pokemon ; type : lista tipi 
    data() {
      return {
        buttons : [],
        searchP : "",
        filteredList : this.list,
        id : "",
      }
    },
    methods: {
      page(vet){
        this.filteredList = []; //permette di visualizzare al click di un nuovo slot di pokemon 
        //dopo aver effettuato una ricerca da input text in header

        console.log("emit value : " , vet);
        this.$emit('clicked',vet); //vet -> emit -> interval
        
         for(let i=vet ; i <= (vet+20) ; i++){
            console.log("indice i di vet : ", i);
            this.$refs.Card[i].img_type_Getter();  
          }
        
      },

      searchPokemon(text) {
        console.log(text);
        this.searchP = text.toLowerCase();
        console.log(this.searchP);
        this.filteredList = [];
        let obj = {};
        let nome = "";
        let url = "";
        let id = "";
        this.list.forEach((element) => {
          // console.log(element);
          if(element.name.includes(this.searchP)){
            console.log(element);
            axios
              .get(element.url)
              .then(response =>{
                nome = element.name; //nome pokemon
                url = element.url; //url pokemon
                id = response.data.id;  //id pokemon
                obj = {nome , url , id}
                this.filteredList.push(obj);
                console.log(response.data.id);
                        
              })
          }
         
        });
        console.log(this.filteredList);

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
// @import 'scss/colors.scss';
.button_container_wrap{
  height: 7%;
}
.button_container{
  overflow-x: scroll;
  display: flex;
}
.button_container::-webkit-scrollbar{
  background-color: transparent;
}
.button_container::-webkit-scrollbar-thumb{
  background: var(--transparent-grey);
  border-radius: 10px !important;
}

.test_button{
  padding: 0px 5px;
  color: var(--grey);
}
.home_wrap {
  height: 100vh;
  background-image: url('../assets/images/home_bg2.jpg');
  background-size: initial;
  background-position: cover;
  background-repeat: no-repeat;
  .home_content{
    height: 100%;
    .header_wrap{
      height: 35%;
    }
    .main_content_wrap{
      height: 57%;
      box-shadow: -1px 1px 5px 9px var(--ultra-transparent-grey);
      .card_wrap{
        height: max-content;

      }
    }
  }
}
</style>