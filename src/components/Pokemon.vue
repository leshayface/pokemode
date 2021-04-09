<template>
  <div>
    <h1>PokeMODE</h1>
    <!-- pass in data to be used as props in PokemonList  -->
    <PokemonList :imageUrl="imageUrl" :apiUrl="apiUrl" />
  </div>
</template>

<script>
import PokemonList from "./PokemonList";

export default {
  data: () => {
    return {
      //store urls for use in other components
      imageUrl: "https://pokeres.bastionbot.org/images/pokemon/",
      apiUrl: "https://pokeapi.co/api/v2/pokemon", //url to fetch data for pokemon
    };
  },
  components: {
    // add any imported components here
    PokemonList,
  },
};
</script>
