<template>
    <h1>¿ Quién es este pokemon? </h1>
    <!-- TODO: img -->
    <PokemonPicture :pokemonId="26" :showPokemon="true" />

    <!-- TODO: opciones -->
    <PokemonOptions :pokemons="pokemonArr"/>

</template>

<script>
import PokemonPicture from '@/components/PokemonPicture'
import PokemonOptions from '@/components/PokemonOptions'

import getPokemonOptions from '../helpers/getPokemonOptions'


export default {
    components: { PokemonPicture, PokemonOptions },
    data() {
        return {
            pokemonArr: []
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions()
        }
    },
    mounted() {
        this.mixPokemonArray()
    }
}
</script>

