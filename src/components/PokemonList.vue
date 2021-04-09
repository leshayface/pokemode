<template>
  <div>
    <h3>Pokemon List</h3>

    <article v-for="(pokemon, index) in pokemons" :key="'poke' + index">
      <img
        :src="imageUrl + pokemon.id + '.png'"
        width="96"
        height="96"
        alt=""
      />
      <h5>{{ pokemon.name }}</h5>
    </article>
  </div>
</template>

<script>
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
  },
  created() {
    this.fetchPokemon();
  },
};
</script>

<style></style>
