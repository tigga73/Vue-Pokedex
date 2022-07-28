<template>
  <ul class="pokedex">
    <li
      class="card"
      v-for="pokemon in pokemonsList"
      :class="pokemon.types[0].type.name"
      :key="pokemon.id"
    >
      <img
        class="card-image"
        :src="pokemon.sprites.other.dream_world.front_default"
        :alt="pokemon.name"
      />
      <h2 class="card-title">{{ pokemon.id }}. {{ pokemon.name }}</h2>
      <p class="card-subtitle">
        {{ pokemon.types.map((typeInfo) => typeInfo.type.name).join(" | ") }}
      </p>
    </li>
  </ul>
</template>
<script>
export default {
  props: ["pokemonsList"],
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

.card-subtitle {
  margin-top: 5px;
  color: #333;
  font-weight: 300;
  position: relative;
  z-index: 2;
}

.card-image {
  width: 200px;
  height: 140px;
  position: relative;
  z-index: 2;
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
