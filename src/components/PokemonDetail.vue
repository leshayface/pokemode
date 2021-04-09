<template>
  <div style="background: blue; width: 100px; height: 200px;">
    <h2 v-if="pokemon">{{ pokemon.name }}</h2>
    <h2 v-else>The pokemon was not found</h2>
    <button class="close" @click="closeDetail">close</button>
  </div>
</template>

<script>
export default {
  props: ["pokemonUrl", "imageUrl"],
  data: () => {
    return {
      pokemon: {},
    };
  },
  //now we can fetch data from the url we passed down
  methods: {
    fetchData() {
      let req = new Request(this.pokemonUrl);
      fetch(req)
        .then((resp) => {
          if (resp.status === 200) return resp.json();
        })
        .then((data) => {
          this.pokemon = data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    closeDetail() {
      this.$emit("closeDetail");
    },
  },
  created() {
    this.fetchData();
  },
};
</script>
