<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>

  <div v-else>
    <h1>¿Quién es este pokemón?</h1>

    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions :pokemons="pokemonArr" @selection="checkAnswer" />

    <div v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>

      <button @click="newGame" class="btn">Nuevo Juego</button>

    </div>
  </div>
</template>

<script>
import PokemonOptions from "../components/PokemonOptions.vue";
import PokemonPicture from "../components/PokemonPicture.vue";
import getPokemonOptions from "../helpers/getPokemonOptions";

// console.log(getPokemonOptions());

export default {
  components: { PokemonOptions, PokemonPicture },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(selectedId) {
      this.showPokemon = true;
      this.showAnswer = true;

      if (selectedId === this.pokemon.id) {
        this.message = `Correcto, ${this.pokemon.name}`;
      } else {
        this.message = `Oops, era ${this.pokemon.name}`;
      }
    },
    newGame() {

      this.showPokemon = false
      this.showAnswer = false
      this.pokemonArr = []
      this.pokemon = null
      this.mixPokemonArray()

    }
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>

<style scoped>

/* CSS */
.btn {
  background-color: #fbeee0;
  border: 2px solid #422800;
  border-radius: 30px;
  box-shadow: #422800 4px 4px 0 0;
  color: #422800;
  cursor: pointer;
  display: inline-block;
  font-weight: 600;
  font-size: 18px;
  padding: 0 18px;
  line-height: 50px;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.btn:hover {
  background-color: #fff;
}

.btn:active {
  box-shadow: #422800 2px 2px 0 0;
  transform: translate(2px, 2px);
}

@media (min-width: 768px) {
  .btn {
    min-width: 120px;
    padding: 0 25px;
  }
}
</style>
