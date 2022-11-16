<template>
  <div class="container">
    <PokemonSearch v-on:searchPokemonEmit="setPokemonSearch" />
    <PokemonDetail v-bind:pokemonUrl="pokemon.url" v-on:closeDetail="close()" v-if="show"/>
    <PokemonList v-on:showPokemonDetailEmit="open" v-bind:pokemonSearch="pokemonSearch" />
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {
   data: ()=>{
    return {
      show : false,
      pokemon : "",
      pokemonSearch: "",
    }
  },
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },
  methods : {
    close : function(){
      this.show = false
    },
    open : function(pkm){
      this.show = true
      // console.log(pkm)
      this.pokemon = pkm
    },
    setPokemonSearch: function(pkmSearch){
      this.pokemonSearch = pkmSearch
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>