<template>
  <div class="home">
    <pkmnList :id="20" :offset="0"></pkmnList>
  </div>
</template>

<script>
import pkmnList from "../components/pkmList.vue";

export default {
  name: "Home",
  components: {
    pkmnList,
  },
};
</script>
