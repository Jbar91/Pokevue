<template>
  <section id="main-display">
    <div id="logo">
      <img
        src="./assets/imgs/Pokemon_logo.png"
        alt="Pokemon Logo"
        id="main-logo"
      />
      <img src="./assets/imgs/pokeball.png" alt="Pokeball" id="pokeball" />
    </div>
  </section>
  <section id="pokemon-display">
    <div
      v-for="(pokemon, index) in poke"
      :key="pokemon"
      class="card"
      :id="pokemon.name"
    >
      <p>{{ pokemon.name }}</p>
      <p>{{ index }}</p>
      <p>{{ pokemon.url }}</p>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  created() {
    axios.get(this.pokeApi).then((response) => {
      /* console.log(
          response.data.results
        );
        Array containing all pokemons specifics urls*/
      this.poke = [...response.data.results];
      // console.log(this.poke);
      for (let i = 1; i < 152; i++) {
        fetch(`https://pokeapi.co/api/v2/pokemon/${i}/`)
          .then((response) => response.json())
          .then((results) => {
            this.pokemonsData.push({
              name: results.name,
              index: i,
            });
          });
      }
      // this.poke.forEach((data) => {
      //   axios.get(data.url).then((result) => {
      //     // console.log(data.url);
      //     this.pokemonsData.push({
      //       name: result.data.name,
      //     });
      //   });
      // });
      console.log(this.pokemonsData);
    });
  },
  data() {
    return {
      pokeApi: "https://pokeapi.co/api/v2/pokemon/?limit=151&?order=1",
      specific: "",
      pokemonsData: [],
      poke: [],
      // pokeUrls: this.pokemons.url,
    };
  },
  computed: {},
};
</script>

<style>
@import url("./styles/styles.css");
</style>
