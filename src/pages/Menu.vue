<script >
  import {state} from '../state.js';
  import axios from 'axios'
  import sh from '../components/SHeader.vue'

  export default {
    components:{sh},

    data(){
        return{     
            state,
            arrProduct:[],
            arrCategory:[],
            categoryId: 0,
        }
    },
    methods:{
      getProduct(cat){
        this.categoryId = cat,
        axios
				.get(state.baseUrl + 'api/projects', {
					params: {
						category: this.categoryId,
					},
				})
				.then(response => {
					this.arrProduct = response.data.results.data;
				});
      },
      getCategory(){
        axios
				.get(state.baseUrl + 'api/categories', {})
				.then(response => {
					this.arrCategory = response.data.results;
				});
        this.arrCategory = this.arrCategory.shift()
      },
      changeCategory(value){

        this.getProduct(value)
      },
      getPrice(cent){
        let num = parseFloat(cent);
        num = num / 100;
        num = "€" + num  

        return num
      },
      fixtag(arr){
      let arrtag='';
      arr.forEach((element, i) => {
        
        if(i+1==arr.length){
           
          arrtag = arrtag + element.name + '.'
        }else{
          arrtag = arrtag + element.name + ', '
          
        }
      });
      return arrtag
      },



    },
    created(){
      this.getProduct(0);
      this.getCategory();


      this.state.actvPage = 2;
    },
    
  }
</script>

<template>
  <div class="menu">
    <sh/>
    <div class="menu-cont">

      <h1>Menu</h1>
      <div class="top-menu">
        <div v-for="cat in arrCategory" class="categry">{{ cat.name }}</div>
      </div>
  
      <div class="main-menu">
  
       <div class="card" v-for="item in arrProduct">
        <img :src="state.getImageUrl(item.image)" alt="">
        <div class="title">{{ item.name }}</div>
        <div class="c-tp">

          <div class="tags"> {{fixtag(item.tags) }}</div>
          <div class="price">{{ getPrice(item.price) }}</div>
        </div>
       </div>
  
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;


.menu-cont::-webkit-scrollbar{
      
      width: 10px;
      height: 10px;
      
  }

.menu-cont::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;
    
}
.menu-cont::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);
    
}
.menu-cont::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;
    
}
.hd{box-shadow: 10px 10px 10px black; }

.menu{
  overflow: hidden;
  height: 100vh;
  display: flex;
  flex-direction: column;

  .menu-cont{
    overflow: auto;
    height: 100%;

    padding: 1rem 0 ;
    .main-menu{

      @include dfc;
      flex-wrap: wrap;
      gap: 1rem;
      .card{
        height: 100px;
        width: calc((100% - 2rem) / 2);

        border-radius: 100px 0 0 100px  ;
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-end;
        overflow: hidden;
        //gap: 1rem;
        //padding: 1rem;
        
        img{
          position: absolute;
          top: 0;
          left: 0;
          height: 100%;
          border-radius: 100px;
        }
        .title{
          padding: 1rem;
          text-align: left;
          width: calc((100% - 100px));
          
        }
        .c-tp{
          background-color: #410606;
          border-radius: 10px;
          width: 100%;
          height: 100%;
          display: flex;
          flex-direction: column;
          justify-content: space-between;
          align-items: flex-end;
          
          .tags, .price{
            border-radius: 10px;
            width: calc((100% - 120px));
            padding-right: .5rem;
            padding-bottom: .5rem;
          }
          .tags{
            white-space: nowrap;
            display: flex;
            padding-top: .5rem;
            overflow: hidden;
            white-space: nowrap;
            text-overflow: ellipsis;
            font-size: 10px;
            font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
            font-weight: bold!important; 
          }
          .price{
            width: 100%;
            //border-radius: 10px ;
            text-align: right;
  
          }
        }
      }

    }
    
  }
}
@media (max-width:$bp1) {
  .card{
    width: calc((100% - 3rem) / 3);
  }
}
</style>
