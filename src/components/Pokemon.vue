<template>
  <div class="flex flex-col items-center p-10">
    <img class="w-1/4 h-auto" alt="Vue logo" src="@/assets/logo.png" />
    <!-- pass in data to be used as props in PokemonList  -->
    <!-- passing setPokemonUrl with current pokemon url argument up from child to parent to use here as method -->
    <PokemonList
      :imageUrl="imageUrl"
      :apiUrl="apiUrl"
      @setPokemonUrl="setPokemonUrl"
    />

    <!-- passing closeModal up from child to parent to use here as method -->
    <PokemonDetail
      v-if="showModal"
      :pokemonUrl="pokemonUrl"
      :imageUrl="imageUrl"
      @closeModal="closeModal"
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
      showModal: false,
    };
  },
  methods: {
    // we have access to the SetPokemonUrl method now as we emitted it to here
    setPokemonUrl(url) {
      //this function sets our defailt data values
      this.pokemonUrl = url;
      this.showModal = true;
    },
    closeModal() {
      this.pokemonUrl = "";
      this.showModal = false;
    },
  },
  components: {
    // add any imported components here
    PokemonList,
    PokemonDetail,
  },
};
</script>
