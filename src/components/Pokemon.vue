<template>
  <div id="pokemons">
    
  <div class="card">
  <div class="card-image">
    <figure >
      <img :src="pokemons.front" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
       
      </div>
      <div class="media-content">
         <h1 class="title is-4"> {{name | upper}} {{num}}</h1>
      </div>
    </div>

    <div class="content">
  
   
    </div>
  </div>
</div>
  </div>
     
</template>

<script>
import axios from 'axios';
export default {
    created: function(){
      axios.get(this.url).then(res=> {
        this.pokemons.type = res.data.types[0].type.name;
        this.pokemons.front = res.data.sprites.front_default;
        this.pokemons.back = res.data.sprites.back_default;
      })
    },
    data(){
      return{
        pokemons: {
          type: '',
          front:'',
          back:''
        }
      }
    },
    props:{
      num:Number,
      name:String,
      url:String
    },
    filters:{
      upper: function(value){
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}
</script>
<style scoped>
  #pokemons{
    margin-top: 3%;
  }
</style>
