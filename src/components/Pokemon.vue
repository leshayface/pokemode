<template>
  <div>
    <h1>PokeMODE</h1>
    <!-- pass in data to be used as props in PokemonList  -->
    <!-- passing setPokemonUrl with current pokemon url argument up from child to parent to use here as method -->
    <PokemonList
      v-if="!showDetail"
      :imageUrl="imageUrl"
      :apiUrl="apiUrl"
      @setPokemonUrl="setPokemonUrl"
    />

    <!-- passing closeDetail up from child to parent to use here as method -->
    <PokemonDetail
      v-if="showDetail"
      :pokemonUrl="pokemonUrl"
      :imageUrl="imageUrl"
      @closeDetail="closeDetail"
    />
  </div>
</template>

<script>
import PokemonList from "./PokemonList";
import PokemonDetail from "./PokemonDetail.vue";

export default {
  data: () => {
    return {
      //store urls for use in other components
      imageUrl: "https://pokeres.bastionbot.org/images/pokemon/",
      apiUrl: "https://pokeapi.co/api/v2/pokemon", //url to fetch data for pokemon
      //default states for data to be passed to details page:
      pokemonUrl: "",
      showDetail: false,
    };
  },
  methods: {
    // we have access to the SetPokemonUrl method now as we emitted it to here
    setPokemonUrl(url) {
      //this function sets our defailt data values
      this.pokemonUrl = url;
      this.showDetail = true;
    },
    closeDetail() {
      this.pokemonUrl = "";
      this.showDetail = false;
    },
  },
  components: {
    // add any imported components here
    PokemonList,
    PokemonDetail,
  },
};
</script>
