<template>
  <v-app>
    <v-container>
      <v-text-field
        v-model="search"
        label="Pesquisar"
        placeholder="Ex: Pikachu"
        solo
      ></v-text-field>
      <pokemon-list :pokemonsList="filteredPokemonList"></pokemon-list>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";
import PokemonList from "./components/PokemonList.vue";
export default {
  name: "App",

  components: {
    "pokemon-list": PokemonList,
  },

  data: () => ({
    pokemons: [],
    search: "",
  }),

  mounted() {
    let listPokemonsUrls = [];
    Array(150)
      .fill()
      .map((_, id) =>
        listPokemonsUrls.push(`https://pokeapi.co/api/v2/pokemon/${id + 1}`)
      );

    axios
      .all(listPokemonsUrls.map((endpoint) => axios.get(endpoint)))
      .then((response) => {
        response.map((pokemon) => this.pokemons.push(pokemon.data));
      });
  },

  computed: {
    filteredPokemonList() {
      return this.pokemons.filter((pokemon) =>
        pokemon.name.includes(this.search)
      );
    },
  },
};
</script>
<style>
#app {
  background: linear-gradient(
      to bottom right,
      rgba(10, 10, 10, 1),
      rgba(12, 39, 63, 1)
    )
    no-repeat center center fixed !important;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover !important;
  background-position: center;
  min-height: 100vh;
}
</style>
