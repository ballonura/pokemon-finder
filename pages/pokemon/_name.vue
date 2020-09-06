<template>
  <div class="container flex flex-col">
    <img class="mt-4" :src="data.sprites.other.dream_world.front_default" />
    <h1 class="mt-4 text-3xl font-semibold capitalize">
      {{ data.species.name }}
    </h1>
    <div class="mt-2 flex items-center">
      <!-- prettier-ignore -->
      <svg class="w-5 fill-current text-yellow-500 mr-1" viewBox="0 0 24 24"><path d="M12 .587l3.668 7.568 8.332 1.151-6.064 5.828 1.48 8.279-7.416-3.967-7.417 3.967 1.481-8.279-6.064-5.828 8.332-1.151z"/></svg>
      <p class="text-sm font-medium">{{ data.base_experience }}</p>
    </div>
    <div class="flex mt-4">
      <p class="mr-4">Weight: {{ data.weight }}</p>
      <p>Height: {{ data.height }}</p>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, $axios }) {
    const { data } = await $axios.get(
      `https://pokeapi.co/api/v2/pokemon/${params.name}`
    );

    return {
      data
    };
  }
};
</script>

<style></style>
