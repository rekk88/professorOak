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
            <div>
              <a href="Pagina.vue">seconda pagina</a>
            </div>
          </div>
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
// import Pagina from './Pagina.vue'
export default {
    name: 'Home',
    
    components: {
      Logo,
      Header,
      Card,
      Sidebar,
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
         
          // let descr         = "";
          // let type1         = "";
          // let type2         = "";
          // let stronzo = "";
          // let descrUrl = "https://pokeapi.co/api/v2/pokemon-species/"+this.readId( pokemon.url )+"/";
          let pokemonID = this.readId(pokemon.url);
          console.log(pokemonID);
          console.log(pokemon);
          // this.fList.push({...pokemon, descr, type1, type2,stronzo });

          // let response1 = await axios.get(descrUrl);
          // let response2 = await axios.get(pokemon.url);
          // type1 = response2.data.types[0].type;
          // if (response2.data.types.length == 2) {
          //   type2 = response2.data.types[1].type;
          // }
          // else type2 = '';
          this.fList.push({...pokemon,pokemonID});
          setTimeout(() => {
            this.show =false;
          }, 300);
          setTimeout(() => {
            this.show=true;
          }, 500);
          // console.log(response1.data);
          // console.log(response2.data);


          // setTimeout(()=>{
          //    response1.data.flavor_text_entries.forEach(element =>{
          //     if(element.language.name == "en"){
          //         descr = element.flavor_text;
          //       }
          //     });
          // type1 = response2.data.types[0].type;
          // stronzo = response2.data.id;
          // if (response2.data.types.length == 2) {
          //   type2 = response2.data.types[1].type;
          // }
          // else type2 = '';
          //   setTimeout(()=>{
          //     this.fList.push({...pokemon, descr, type1, type2,stronzo });
          //     this.testId.push(response2.data.id);
          //   },0);
          // },500);
         
          //console.log(pokemon.name);

          
          // axios.all([
          //         await axios.get(pokemon.url), //chiamata per sprite e tipo del singolo pokemon
          //         await axios.get(descrUrl) //chiamata per la descrizione del pokemon
          // ])
          // .then(axios.spread((obj1, obj2)=>{  
              
          //       obj2.data.flavor_text_entries.forEach(element => {
                  
          //         if(element.language.name == "en"){
          //             descr = element.flavor_text;
                      
          //         }
          //       });

          //       type1 = obj1.data.types[0].type;
          //       stronzo = obj2.data.id;
          //       if (obj1.data.types.length == 2) {
          //           type2 = obj1.data.types[1].type;
          //       }

          //       else type2 = '';
          //       setTimeout(()=>{
          //         this.fList.push({...pokemon, descr, type1, type2,stronzo });
          //         this.testId.push(obj2.data.id);
          //       },500);
          //       // console.log(pokemon.name);

          // }));               

      },

      async reloadList()
      {
            this.render = false;
            this.sorted3 = false;
            this.sortedList = [];
            // this.show = false;
            setTimeout(()=>{ 
              //  this.list.forEach((element) => {
              //     // setTimeout(300);
              //     this.loadPokemon( element )            
              //  });

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
    //   if (this.sorted) {
    //    console.log("updated hook ids : ",this.testId);
        
    //   }
    //   // sorting objects array
    //   if (this.fList.length == 20) {
    //     console.log("updated",this.fList.length);
    //     console.log("updated flist : ",this.fList);
    //     // this.copiaLista = this.fList;
    //     console.log("copia array : ",this.copiaLista);
    //     // setTimeout(()=>{
    //       // console.log("timeout");

    //      for(let f = 0; f < this.fList.length; f++) {
    //         for(let j = 0; j < this.fList.length - 1; j++) {
    //           console.log("for");
    //           // if (j < 19) {
    //             if(this.fList[j].stronzo > this.fList[j+1].stronzo){
    //               let temp = this.fList[j];
    //               this.fList[j] = this.fList[j+1];
    //               this.fList[j+1] = temp;
    //             }
    //           // }
              
    //         }
    //       }
    //       this.sorted2 = true;
    //       this.sorted3 = true;
    //       // if (this.sorted3== true && this.render==false) {
    //       //   // this.cardKey += 1; //re render key
    //       // }
    //       if (this.sorted3) {
    //               console.log("sorted array : ",this.fList);          
    //       }
    //       this.sortedList = this.fList;
    //     // },100);
        
       
    //   }
      
    // },
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