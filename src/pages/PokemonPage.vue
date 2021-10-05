<template>
    <h1>¿ Quién es este pokemon? </h1>
    <!-- TODO: img -->
    <PokemonPicture :pokemonId="4" :showPokemon="false" />

    <!-- TODO: opciones -->
    <PokemonOptions />

</template>

<script>
import PokemonPicture from '@/components/PokemonPicture'
import PokemonOptions from '@/components/PokemonOptions'

export default {
    components: { PokemonPicture, PokemonOptions }
}
</script>

