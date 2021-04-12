<template>
  <div>
    <div v-if="loading">
      <Spinner />
    </div>
    <div v-else>
      <div class="flex flex-col items-center space-y-4">
        <span class="hidden">{{ (Poki = randomPokemon()) }}</span>
        <h2 class="text-2xl">Your lucky Pokemon of the second is:</h2>
        <img :src="imageUrl + Poki.id + '.png'" width="96" height="96" alt="" />
        <h4 class="text-xl font-bold">
          {{ Poki.name.toUpperCase() }}
        </h4>
      </div>
      <!-- The @click is emiting the current pokemon url with id to the parent component -->
      <div
        class="grid grid-cols-1 gap-5 sm:gap-10 sm:grid-cols-2 lg:grid-cols-4 mt-20"
      >
        <article
          class="flex flex-col items-center bg-white rounded-lg shadow p-6 cursor-pointer"
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
    </div>
  </div>
</template>

<script>
import Url from "./Url";
import Spinner from "./spinner.vue";

export default {
  data: () => {
    return {
      pokemons: [],
      loading: false,
    };
  },
  props: [
    //passed props from Pokemon.vue
    "imageUrl",
    "apiUrl",
  ],
  components: {
    Url,
    Spinner,
  },
  methods: {
    fetchPokemon() {
      // fetch(this.apiUrl)
      //   .then((response) => response.json())
      //   .then((allpokemon) => console.log(allpokemon));

      // access props with this.
      let req = new Request(this.apiUrl);
      this.loading = true;
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
        })
        .finally(() => (this.loading = false));
    },
    setPokemonUrl(url) {
      this.$emit("setPokemonUrl", url);
    },
    randomPokemon() {
      return this.pokemons[Math.floor(Math.random() * this.pokemons.length)];
    },
  },
  created() {
    this.fetchPokemon();
  },
};
</script>

<style></style>
