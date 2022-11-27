<template>
  <div class="list">
    <article v-for="pkm in pokemonsFiltered" v-bind:key="pkm.name" v-on:click="showPokemonDetail(pkm)">
      <img v-bind:src="images+'/'+pkm.name+'.png'">
      <h3>{{pkm.name}}</h3>
    </article>
  </div>
</template>

<script>
import config from '../config/config.json'
import axios from 'axios'
import lodash from 'lodash'
export default {
  data: ()=>{
    return {
      pokemons : [],
      images : config.IMG_URL,
    }
  },
  computed: {
    pokemonsFiltered: function () {
      const regex = new RegExp(this.pokemonSearch+'\\.*');
      if (this.pokemonSearch=="") {
        return this.pokemons
      } else {
        return lodash.filter(this.pokemons, function(pkm){return regex.test(pkm.name)})
      }
    },
  },
  methods : {
    showPokemonDetail : function(pkm){
      this.$emit("showPokemonDetailEmit",pkm)
    },
  },
  props : ['pokemonSearch'],
  beforeMount(){
    axios.get(config.API_URL+'/pokemon?offset=0&limit=721')
    .then((response) => {
      console.log(response);
      this.pokemons = response.data.results;
      // console.log(this.pokemons)
    })
    .catch((error) => {
        console.log(error)
    });
  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
article:hover {
  background-color: #c5c1c1;
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

