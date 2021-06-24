<template>
  <div class="container">
    <div class="poke-card">
      <h2>{{ singlePokemon.name }}</h2>
      <img :src="sprite" alt="" />
      <h3 :style="backgroundColor">{{ singlePokemon.types[0].type.name }}</h3>
      <ul>
        <li v-for="stat in stats" :key="stat" class="poke-stat">
          <div :style="backgroundColor">{{ stat.stat.name }}</div>
          <div :style="backgroundColor">{{ stat.base_stat }}</div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      singlePokemon: {},
      stats: [],
      typeColor: "",
      colors: {
        fire: "#FD7D24",
        grass: "#9BCC50",
        electric: "#EED535",
        water: "#4592C4",
        ground: "#A38C21",
        rock: "#A38C21",
        fairy: "#FDB9E9",
        poison: "#B97FC9",
        ghost: "#B97FC9",
        bug: "#729F3F",
        dragon: "#7766EE",
        psychic: "#F366B9",
        flying: "#BDB9B8",
        fighting: "#D56723",
        normal: "#999",
        ice: "#51C4E7",
        steel: "#AAAABB",
        dark: "#775544",
      },
    };
  },
  computed: {
    sprite: function () {
      return `https://pokeres.bastionbot.org/images/pokemon/${this.singlePokemon.id}.png`;
    },
    backgroundColor: function () {
      return "background-color: " + this.colors[`${this.typeColor}`];
    },
  },
  mounted: function () {
    this.fetchData();
  },
  methods: {
    fetchData: async function () {
      try {
        const result = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${this.$route.params.id}`
        );
        const singlePokemon = await result.json();
        this.singlePokemon = singlePokemon;

        this.stats = singlePokemon.stats;
        this.typeColor = this.singlePokemon.types[0].type.name;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style lang="scss">
body {
  background-color: #111;
}
.container {
  background-color: #111;
  height: 100vh;
  width: 100vw;
}
h2 {
  font-size: 3rem;
  text-transform: uppercase;
  transform: translateZ(20px);
}
h3 {
  font-size: 4rem;
  text-transform: uppercase;
  padding: 3rem 6rem;
  transform: translateZ(20px);
  color: #fff;
}
.poke-card {
  background-color: #fff;
  transform-style: preserve-3d;
  box-shadow: 0 0 30px 10px #aaa;
  padding: 2rem;
  width: 45vw;
  margin: 10rem auto;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}
img {
  margin: 1rem auto;
  width: 22rem;
}
/* li:nth-of-type(1) {
  grid-area: HP;
}
li:nth-of-type(2) {
  grid-area: Attack;
}
li:nth-of-type(3) {
  grid-area: Defense;
}
li:nth-of-type(4) {
  grid-area: spattack;
}
li:nth-of-type(5) {
  grid-area: spedefense;
}
li:nth-of-type(6) {
  grid-area: speed;
}
 */
.poke-stats {
  margin: 2rem auto;
  text-transform: uppercase;
  transform: translateZ(20px);
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}
.poke-stat {
  font-size: 2rem;
  width: 40%;
  list-style: none;
  padding: 2rem;
  transform: translateZ(20px);
  color: black;
}
.poke-stat div {
  padding: 5px;
  transform: translateZ(20px);
  font-size: 2rem;
}
.back-btn {
  color: #fff;
  font-size: 3rem;
}
.zoom-enter-active,
.zoom-leave-active {
  animation-duration: 0.3s;
  animation-name: zoom;
}
.zoom-enter,
.zoom-leave-to {
  animation-name: zoom;
}
@keyframes zoom {
  from {
    opacity: 0;
    transform: scale3d(0.3, 0.3, 0.3);
  }
  100% {
    opacity: 1;
  }
}
</style>
