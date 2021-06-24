<template>
  <div>
    <ul class="pokemon-table">
      <li
        class="pokemon-list-item"
        v-for="pokemon in pokemons"
        :key="pokemon.name"
      >
        <pkmn-preview :pokemon="pokemon"></pkmn-preview>
      </li>
    </ul>
  </div>
</template>

<script>
import pkmnPreview from "./pkmnPreview.vue";

export default {
  name: "pkmnList",
  data() {
    return {
      pokemons: [],
    };
  },
  props: ["id", "offset"],
  created: function () {
    this.fetchData();
  },
  methods: {
    fetchData: async function () {
      try {
        const result = await fetch(
          `https://pokeapi.co/api/v2/pokemon?limit=${this.id}&offset=${this.offset}`
        );
        const data = await result.json();
        console.log(data);
        this.pokemons = data.results; //Must remember to change this value
      } catch (error) {
        alert(error);
      }
    },
  },
  components: {
    pkmnPreview,
  },
};
</script>

<style></style>
