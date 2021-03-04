<template>
  <div id="pokemons">
  <div class="card">
  <div class="card-image">
    <figure >
      <img :src="currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
      </div>
      <div class="media-content">
         <h1 class="title is-4">Nome Pokemon: {{num}} - {{name | upper}}</h1>
         <h2 class="title is-4">Type Pokemon: {{pokemons.type | upper}}</h2>
      </div>
    </div>
    <div class="content">
         <button @click="mudarSprite" class="button is-medium is-fullwidth">Mudar Imagem</button>
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
        this.currentImg = this.pokemons.front;
      })
    },
    data(){
      return{
        isFront: true,
        currentImg: '',
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
  },
  methods:{
    mudarSprite: function(){
      if(this.isFront){
        this.isFront = false;
        this.currentImg = this.pokemons.back;
      }else{
        this.isFront = true;
        this.currentImg = this.pokemons.front;
      }
    }
  }

}
</script>
<style scoped>
  #pokemons{
    margin-top: 3%;
  }
</style>
