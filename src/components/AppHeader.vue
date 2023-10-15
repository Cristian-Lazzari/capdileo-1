
<script >
  import {state} from '../state.js';

 export default{
  data(){
    return{
      state,
    }
  },
  
 }
</script>


<template>
  <div class="header">
    <div class="btn-menu" @click="state.openside">Menu</div>
    <div class="cont">
      <div class="center">
        <h1 id="title">Il Capriccio <br> di Leo</h1>
        <img src="../assets/img/pizza-olio.png" alt="">
      </div>
      <div class="par" v-if="state.setting[2].status" >
        Finalmente un po di riposo anche per noi.. siamo in ferie dal {{ state.setting[2].from }} e torneremo il  {{ state.setting[2].to }}
      </div>
    </div>
    </div>
</template>

<style lang="scss" scoped>
@use '../assets/styles/general.scss' as *;
.btn-menu{
  display: none;
  margin-left: 10px;
  text-transform: uppercase;
  background-color: $c-footer-nav;
  color: $c-nav-link;
  font-weight: bolder;
  width: fit-content;
  padding: 1rem 2rem;
  border-radius: 0 0 20px 20px ;

}
.header{
  background-color: $c-header;
  margin-left: 2rem;
  height: 40%;
  
  .cont{
    @include dfc;
    flex-direction: column;
    justify-content: space-between;
    height: 80%;
    
    .center{

      height: 80%;
      padding: 0 4rem;
      @include dfc;
      justify-content: space-between;
  
      width: 100%;
  
      h1{
        color: white;
        font-family: 'Playball', cursive;
        font-size: 60px;
        text-shadow: -3px -3px 15px black;
        text-align: center;
      }
      img{
        box-shadow: -7px -7px 20px black;
        position: relative;
        height: 100%;
        //height: 80px;
      }
    }
  }
  
}
.par{
  color: white;
  text-shadow: 2px 2px 6px black;
  padding-bottom: 1em;
}

@media (max-width:$bp1) {

  .btn-menu{
    display: block;
  }
  .header{
    margin: 0;
  }
  
}
@media (max-width:$bp2){
  .header{
    background-image: url('../assets/img/pizza-espansa.png');
    background-position: center;
    background-size: cover;
    .cont{
  
      backdrop-filter: blur(5px);
    }
    .center{
      justify-content: center!important;
    }
    img{
      display: none;
   
    }
  }
}

@media (max-width:$bp3) {
  
  #title{
    font-size: 40px;
  }
  
}


</style>
