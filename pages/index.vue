<template>
  <div class="flex flex-col container max-h-screen">
    <img class="w-32 mx-auto mt-4" src="@/assets/images/logo.png" />
    <input
      class="shadow-lg rounded-full mt-4 px-4 h-12 focus:outline-none flex-shrink-0"
      type="text"
      v-model="q"
      placeholder="What pokemon are you search for?"
    />
    <div class="mt-4 overflow-y-auto">
      <nuxt-link
        v-for="(pokemon, index) in filteredPokemonList"
        :key="pokemon.name"
        :to="`/pokemon/${pokemon.name}`"
        class="block capitalize font-medium border-b border-gray-300 py-2"
      >
        <p>
          {{ index }}.
          {{ pokemon.name }}
        </p>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  async mounted() {
    const {
      data: { results },
    } = await this.$axios.get("https://pokeapi.co/api/v2/pokemon?limit=1050");
    this.pokemonList = results;
  },
  data() {
    return {
      q: "",
      pokemonList: [],
    };
  },
  computed: {
    filteredPokemonList() {
      if (this.q && this.q.length >= 2) {
        return this.pokemonList.filter((x) => x.name.includes(this.q));
      } else {
        return this.pokemonList;
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
