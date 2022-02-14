<template>
  <div class="w-full flex justify-center">
    <input
      type="text"
      placeholder="Enter pok here..."
      class="mt-10 p-2 border-blue-500 border-2"
      v-model="text"
    />
  </div>
  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div
      class="ml-4 text-2px text-blue-400"
      v-for="(pokemon, idx) in filteredPoke"
      :key="idx"
    >
    <router-link :to="`/about/${uldIdLookup[pokemon.name]}`">
      {{ pokemon.name }}</router-link>
    </div>
  </div>
</template>

<script lang="ts">
const API = "https://pokeapi.co/api/v2/pokemon?offset=0";
import { defineComponent, reactive, toRefs, computed } from "vue";
export default defineComponent({
  name: "HomeView",
  setup() {
    const state = reactive({
      pokemons: [],
      uldIdLookup: {},
      text: "",
      filteredPoke: computed(() => updatePoke()),
    });

    function updatePoke(): any {
      if (!state.text) {
        return [];
      }
      return state.pokemons.filter((pok: any) => pok.name.includes(state.text));
    }

    fetch(API)
      .then((response) => response.json())
      .then((data) => {
        state.pokemons = data.results;
        state.uldIdLookup = data.results.reduce(
          (acc: any, cur: any, idx: any) =>
            (acc = { ...acc, [cur.name]: idx + 1 }),
          {}
        );
      });
    return { ...toRefs(state) };
  },
});
</script>
