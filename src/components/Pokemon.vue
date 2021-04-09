<template>
  <div class="container">
    <h1>Pokemon's</h1>
    <PokemonList
      v-if="!showDetail"
      :imageUrl="imageUrl"
      :apiUrl="apiUrl"
      @setPokemonUrl="setPokemonUrl"
    />
    <PokemonDetail
      v-if="showDetail"
      :pokemonUrl="pokemonUrl"
      :imageUrl="imageUrl"
      @closeDetail="closeDetail"
    />
  </div>
</template>

<script>
import PokemonList from "./PokemonList.vue";
import PokemonDetail from "./PokemonDetail.vue";
export default {
  data: () => {
    return {
      imageUrl:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      apiUrl: "https://pokeapi.co/api/v2/pokemon/",
      pokemonUrl: "",
      showDetail: false,
    };
  },
  components: {
    PokemonList,
    PokemonDetail,
  },
  methods: {
    setPokemonUrl(url) {
      this.pokemonUrl = url;
      this.showDetail = true;
    },
    closeDetail() {
      this.pokemonUrl = "";
      this.showDetail = false;
    },
  },
};
</script>
