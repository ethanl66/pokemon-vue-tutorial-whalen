<template>
  <div>
    <div class="pkmn-container">
      <h1 id="query">{{ pokemon.name }}</h1>
      <img :src="sprite" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  name: "PkmnPreview",
  props: ["pokemon"],
  data() {
    return {
      singlePokemon: {},
    };
  },
  mounted: function () {
    this.fetchData();
    console.log(this.singlePokemon);
  },
  methods: {
    fetchData: async function () {
      try {
        const result = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${this.pokemon.name}`
        );
        const singlePokemon = await result.json();
        this.singlePokemon = singlePokemon;
      } catch (error) {
        console.log(error);
      }
    },
  },
  computed: {
    sprite: function () {
      //return this.singlePokemon.sprites.front_default;
      return `https://pokeres.bastionbot.org/images/pokemon/${this.singlePokemon.id}.png`;
    },
  },
};
</script>

<style>
#query {
  color: #111;
  font-size: 2rem;
}
.pkmn-container {
  background-color: #999;
  padding: 2rem;
  color: #111;
}
</style>
