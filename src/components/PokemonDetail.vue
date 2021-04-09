<template>
  <div>
    <transition name="fade" appear>
      <div
        class="fixed z-10 inset-0 overflow-y-auto"
        aria-labelledby="modal-title"
        role="dialog"
      >
        <div
          class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0"
        >
          <div
            class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
          ></div>
          <span class="hidden sm:inline-block sm:align-middle sm:h-screen"
            >&#8203;</span
          >

          <transition name="pop" appear>
            <div
              class="inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-sm sm:w-full sm:p-6"
            >
              <div v-if="pokemon">
                <img :src="imageUrl + pokemon.id + '.png'" alt="" />
                <h2>{{ pokemon.name }}</h2>
              </div>
              <h2 v-else>The pokemon was not found</h2>
              <button
                @click="closeModal"
                class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
              >
                Close
              </button>
            </div>
          </transition>
        </div>
      </div>
    </transition>
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
    closeModal() {
      this.$emit("closeModal");
    },
  },
  created() {
    this.fetchData();
  },
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s linear;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.pop-enter-active,
.pop-leave-active {
  transition: transform 0.5s cubic-bezier(0.5, 0, 0.5, 1), opacity 0.5s linear;
}

.pop-enter,
.pop-leave-to {
  opacity: 0;
  transform: scale(0.3) translateY(-50%);
}
</style>
