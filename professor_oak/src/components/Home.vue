<template>
  <div class="home_wrap pb-4">
    <div class="home_content">
      <div class="header_wrap">
        <Logo/>
        <Header 
          :tipi="type"
          @searchForm="searchPokemon"
        />
      <Footer/>
      </div>
      
      <div class="container text-center mb-3 button_container_wrap">
        <div class="button_container">
          <div class="d-inline-block" v-for="(button,index) in buttons" :key="index">
            <div v-if="index < 44">
              <div class="box_button" id="clicked" @click="page(button)">
                {{button}}-{{button + 20}}
              </div>
            </div>
            <div class="box_button" v-else @click="page(880)">
              881-898
            </div>
          </div>
        </div>
      </div>
      
      <div class="main_content_wrap container d-flex p-0 rounded">
        <div class="col d-none">
          <div class="h_100">
            <div class="p-0 h_100">
              <Sidebar :lista="list" :n="indice"/>
            </div>
          </div>
        </div>
          
        <div class="container d-flex justify-content-center align-items-start col-10 py-3 overflow scrollbar">
          <div>
            <div class="row row-cols-3" :key="cardKey">
                <div class="col card_wrap" v-for="(item, index2) in fList" :key="index2"> 
                  <div class="" v-if="show"> <!--v-if per la ricerca da header -->
                      <Card 
                          :pokemon="item" 
                          :p="show"
                          ref="Card"                    
                      /> 
                  </div>  
                </div>
            </div>
          </div>

        </div>
      </div>
      <!-- creators section --> 
      <div class="made_by text-center">Made By</div>

      <div class="container mt-2 d-flex justify-content-center">
        <div class="creators d-flex">
          <span>
            <img  src="../assets/images/carmelo.jpg" alt="carmelo">
            <span>
              <!-- <i class="bi bi-linkedin"></i> -->
              <a href="https://www.linkedin.com/in/carmelo-granvillano/" target="_blank" class="d-block text-center"><i class="bi bi-linkedin me-2"></i>Carmelo</a>

            </span>
          </span>
          <span class="ms-5">
            <img  src="../assets/images/maicol.jpg" alt="carmelo">
            <span>
              <!-- <i class="bi bi-linkedin"></i> -->
              <a href="https://www.linkedin.com/in/maicolmatteoli/" target="_blank" class="d-block text-center"><i class="bi bi-linkedin me-2"></i>Maicol</a>

            </span>
          </span>
         
        </div>
      </div>
    </div>
  </div>
</template>
          


<script>
// import axios from 'axios'
// import axios from 'axios'
import Card from './Card.vue'
import Header from './Header.vue'
import Logo from './Logo.vue'
import Sidebar from './Sidebar.vue'
import Footer from './Footer.vue'
// import Pagina from './Pagina.vue'
export default {
    name: 'Home',
    
    components: {
      Logo,
      Header,
      Card,
      Sidebar,
      Footer
      // Pagina
    },
    //prop in arrivo da App (con il risultato della chiamata axios)
    props:["list", "type", "indice","staticList"], //list : lista pokemon ; type : lista tipi 
    data() {
      return {
        buttons : [],
        searchP : "",
        fList : [],
        testId : [],
        baseList : this.staticList,
        id : "",
        show : false,
        test : 10,
        sorted : false,
        sorted2 : false,
        sorted3 : false,
        sortedList : [], //test
        cardKey : 0, //re rendering key
        render: false,
        copiaLista : []
      }
    },
    methods: {
      page(vet){
        this.filteredList = []; //permette di visualizzare al click di un nuovo slot di pokemon 
        //dopo aver effettuato una ricerca da input text in header

        console.log("emit value : " , vet);
        this.$emit('clicked',vet); //vet -> emit -> interval
        
        this.reloadList()      
        
      },

       readId:function( url )
      {
          const id_split = url.split('/')
          let id = id_split.pop()
          id = id_split.pop()
        
          return id
      },

      async loadPokemon( pokemon ) //element  = pokemon per reference
      {
          if (this.fList.length > 20) { //tolgo sempre la metà del vettore che non mi serve più
            console.log("slice");
            let firstHalf = this.fList.slice(20, 39);
            this.fList = firstHalf;
            // this.fList = []; //svuoto il vettore
          }
         
          let pokemonID = this.readId(pokemon.url);
          console.log(pokemonID);
          console.log(pokemon);
       
          this.fList.push({...pokemon,pokemonID});
          setTimeout(() => {
            this.show =false;
          }, 200);
          setTimeout(() => {
            this.show=true;
          }, 250);
                     

      },

      async reloadList()
      {
            this.render = false;
            this.sorted3 = false;
            this.sortedList = [];
            // this.show = false;
            setTimeout(()=>{ 
              for(let element of this.list){
                 this.loadPokemon(element)

               }
              this.render = true;
              console.log("delay list : " , this.list);
              // this.testId.sort();
              console.log("id pre sort : ",this.testId);
             
              // let l2 = this.testId.length;
              let firstHalf = this.testId.slice(20, 39);
              this.testId = firstHalf;
              // let l1 = this.testId.length;

         
              console.log("id : ",this.testId);
              // this.fList = this.list;
              this.show = true;

            
            }, 1000);
            // this.cardKey++;

      },

      searchPokemon(text) 
      {

        this.fList = new Array();   

        if(text != ""){
         
          this.searchP  = text.toLowerCase();  
          this.list.forEach((element) => {
            
            if(element.name.includes(this.searchP))
            {
                this.loadPokemon( element )                
            }
          
          });
          
        }
        else{
        
            this.reloadList(); //visualizzazione al caricamento della pagina
        }
        

      } 
    },
   
    mounted() {
   
      for(let i=0 ; i <=880 ; i=i+20){
        this.buttons.push(i);
      }
      // this.fList = this.list
      
      console.log("mounted",this.testId.length);
    },
    created() {
      // this.fList = this.list
      console.log("created",this.fList.length);

      this.reloadList();
      
    },
    updated() {
      //sorting ids array
      // if (this.testId.length == 20) {
      //   console.log("updated",this.testId.length);
      //   for(let f = 0; f < this.testId.length; f++) {
      //     for(let j = 0; j < this.testId.length; j++) {
      //       console.log("for");
      //       if(this.testId[j] > this.testId[j + 1]){
      //         let temp = this.testId[j];
      //         this.testId[j] = this.testId[j + 1];
      //         this.testId[j + 1] = temp;
      //       }
      //     }
      //   }
      //   this.sorted = true;

      //   setTimeout(()=>{
      //     this.index2 = 3;
      //   },2000)
        
      }
    
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
  padding: 15px 0;
}

.button_container::-webkit-scrollbar{
  background-color: transparent;
}
.button_container::-webkit-scrollbar-thumb{
  background: var(--transparent-grey);
  border-radius: 10px !important;
}

.box_button {
  padding: 1px 6px;
  border-radius: 15px;
  color: var(--grey);

  &:hover {
    cursor: pointer;
    color: var(--greenBulba);
    background-color: var(--transparent-grey);
    transition: .15s;
  }
}

#clicked:active { 
  background-color: var(--grey);
}




.home_wrap {
  // height: 100vh;
  height: calc(100vh - 70px);
  // background-image: url('../assets/images/home_bg2.jpg');
  // background-size: initial;
  // background-position: cover;
  // background-repeat: no-repeat;
  .home_content{
    // height: 100%;
    height: calc(100% - 70px);

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