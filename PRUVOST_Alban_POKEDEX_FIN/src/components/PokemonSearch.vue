<template>
  <div class="searchbar">
    <input type="text" placeholder="Rechercher un Pokemon" v-model="pokemonSearch"/>
    <img src="../../public/croix.png" v-on:click="reset()"/>
  </div>
</template>

<script>
export default {
  data: ()=>{
    return {
      pokemonSearch : "",
    }
  },
  watch: {
    pokemonSearch: function(){
      this.$emit("searchPokemonEmit",this.pokemonSearch)
    }
  },
  methods: {
    reset: function(){
      this.pokemonSearch = "";
    }
  },
};
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 510px;
  padding-bottom: 20px;
}
input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
img {
  position: absolute;
  width: 6%;
  margin-left: -40px;
  margin-top: 5px;
  cursor: pointer;
}
</style>
