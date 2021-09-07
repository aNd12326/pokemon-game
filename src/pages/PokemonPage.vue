<template>
    <h1>¿Quien es este pokemón?</h1>
    
    <PokemonPicture :pokemonId="534" :showPokemon="true" />
        
    <PokemonOptions />
</template>

<script>
import PokemonOptions from '../components/PokemonOptions.vue'
import PokemonPicture from '../components/PokemonPicture.vue'
import getPokemonOptions from '../helpers/getPokemonOptions'

console.log(getPokemonOptions());

export default {
    components: { PokemonOptions, PokemonPicture}
}
</script>
