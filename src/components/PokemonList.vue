<template>
  <div>
    <loading-animated v-if="!isLoaded"></loading-animated>
    <ul class="pokedex">
      <li
        class="card"
        v-for="pokemon in pokemonsList"
        :key="pokemon.id"
        :class="pokemon.types[0].type.name"
        @click="showPokemonModal(pokemon)"
      >
        <img
          class="card-image"
          :src="pokemon.sprites.other.dream_world.front_default"
          :alt="pokemon.name"
          @load="onImgLoad"
        />
        <h2 class="card-title">{{ pokemon.id }}. {{ pokemon.name }}</h2>
        <p class="card-subtitle">
          {{ pokemon.types.map((typeInfo) => typeInfo.type.name).join(" | ") }}
        </p>
      </li>
    </ul>
    <v-dialog v-model="showModal" width="50vw">
      <v-card v-if="selectedPokemon">
        <v-btn class="colse-btn-modal" icon @click="showModal = !showModal">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-container class="pa-md-10">
          <v-row>
            <v-col class="flex" cols="6">
              <img
                class="img-responsive"
                :src="selectedPokemon.sprites.other.dream_world.front_default"
                :alt="selectedPokemon.name"
              />
            </v-col>
            <v-col cols="6">
              <h2 class="card-title">{{ selectedPokemon.name }}</h2>
              <p class="card-subtitle">
                {{
                  selectedPokemon.types
                    .map((typeInfo) => typeInfo.type.name)
                    .join(" | ")
                }}
              </p>
              <v-divider class="my-4"></v-divider>
              <v-chip class="mb-2"
                >Altura: {{ selectedPokemon.height / 10 }}m</v-chip
              >
              <v-chip class="ml-2 mb-2"
                >Peso: {{ selectedPokemon.weight }}kg</v-chip
              >
              <h3 class="card-title-sub my-2">Habilidades</h3>
              <ul class="my-2 capitalize-title">
                <li
                  v-for="ability in selectedPokemon.abilities"
                  :key="ability.ability.slot"
                >
                  {{ ability.ability.name }}
                </li>
              </ul>
              <h3 class="card-title-sub my-2">Status</h3>
              <ul class="my-2 capitalize-title">
                <li
                  v-for="status in selectedPokemon.stats"
                  :key="status.stat.name"
                >
                  <b>{{ status.stat.name }}: </b>{{ status.base_stat }}
                </li>
              </ul>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
import LoadingAnimated from "./LoadingAnimated.vue";
export default {
  components: {
    "loading-animated": LoadingAnimated,
  },

  props: ["pokemonsList"],

  data: () => ({
    showModal: false,
    selectedPokemon: null,
    isLoaded: false,
  }),

  methods: {
    showPokemonModal(pokemon) {
      this.selectedPokemon = pokemon;
      this.showModal = !this.showModal;
    },
    onImgLoad() {
      this.isLoaded = true;
    },
  },
};
</script>
<style>
.pokedex {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 13px;
  padding-inline-start: 0;
  padding-left: 0 !important;
}

.card {
  list-style: none;
  padding: 40px;
  color: #222;
  text-align: center;
  border-radius: 20px;
  position: relative;
}

.card::after {
  content: "";
  display: block;
  width: 50%;
  height: 40%;
  border-radius: 100%;
  background-color: #fff;
  opacity: 0.7;
  position: absolute;
  top: 15%;
  left: 25%;
}

.steel {
  background-color: #f4f4f4;
}

.fire {
  background-color: #fbb4b4;
}

.grass {
  background-color: #c1ffc5;
}

.electric {
  background-color: #f9ff98;
}

.water,
.ice {
  background-color: #def3fd;
}

.ground {
  background-color: #cba15e;
}

.rock {
  background-color: #d5d5d4;
}

.fairy {
  background-color: #ffd7fc;
}

.poison {
  background-color: #ca98d7;
}

.bug {
  background-color: #f8d5a3;
}

.dragon {
  background-color: #97b3e6;
}

.psychic {
  background-color: #eaeda1;
}

.flying {
  background-color: #f5f5f5;
}

.fighting {
  background-color: #e6e0d4;
}

.normal {
  background-color: #f5f5f5;
}

.card:hover {
  cursor: pointer;
  animation: bounce 0.5s linear;
}

.ghost > .card-title,
.ghost > .card-subtitle {
  color: #fff;
}

.card-title {
  text-transform: capitalize;
  margin-bottom: 0px;
  font-size: 26px;
  font-weight: normal;
  position: relative;
  z-index: 2;
}

.card-title-sub {
  text-transform: capitalize;
  margin-bottom: 0px;
  font-size: 18px;
  font-weight: normal;
  position: relative;
  z-index: 2;
}

.card-subtitle {
  margin-top: 5px;
  color: #333;
  font-weight: 300;
  position: relative;
  z-index: 2;
  text-transform: capitalize;
}

.card-image {
  width: 200px;
  height: 140px;
  position: relative;
  z-index: 2;
}

.capitalize-title {
  text-transform: capitalize;
}

.img-responsive {
  max-width: 100%;
}

.flex {
  display: flex;
}

.colse-btn-modal {
  float: right;
}

@keyframes bounce {
  20% {
    transform: translateY(-6px);
  }
  40% {
    transform: translateY(0px);
  }

  80% {
    transform: translateY(-2px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>
