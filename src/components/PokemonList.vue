<template>
  <div>
    <h3>Pokemon List</h3>

    <!-- The @click is emiting the current pokemon url with id to the parent component -->
    <article
      v-for="(pokemon, index) in pokemons"
      :key="'poke' + index"
      @click="setPokemonUrl(pokemon.url)"
    >
      <img
        :src="imageUrl + pokemon.id + '.png'"
        width="96"
        height="96"
        alt=""
      />
      <h5>{{ pokemon.name }}</h5>
      <Url :pokurl="pokemon.url" />
    </article>
  </div>
</template>

<script>
import Url from "./Url";

export default {
  data: () => {
    return {
      pokemons: [],
    };
  },
  props: [
    //passed props from Pokemon.vue
    "imageUrl",
    "apiUrl",
  ],
  components: {
    Url,
  },
  methods: {
    fetchPokemon() {
      // fetch(this.apiUrl)
      //   .then((response) => response.json())
      //   .then((allpokemon) => console.log(allpokemon));

      // access props with this.
      let req = new Request(this.apiUrl);
      fetch(req)
        .then((resp) => {
          if (resp.status == 200) return resp.json();
        })
        // .then((allpokemon) => console.log(allpokemon))
        .then((data) => {
          data.results.forEach((pokemon) => {
            //push each pokemon object into pokemons array
            this.pokemons.push(pokemon);
            // we want to get the id at the end of the pokemon.url to use in img src
            pokemon.id = pokemon.url
              .split("/")
              .filter(function(part) {
                return !!part;
              })
              .pop();
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
    setPokemonUrl(url) {
      this.$emit("setPokemonUrl", url);
    },
  },
  created() {
    this.fetchPokemon();
  },
};
</script>

<style></style>
