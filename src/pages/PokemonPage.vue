<template>
    <h1 v-if="!pokemon">Espere por favor...</h1>

    <div v-else>
        <h1>¿ Quién es este pokemon? </h1>

        <!-- TODO: img -->
        <PokemonPicture 
            :pokemonId="pokemon.id" 
            :showPokemon="showPokemon" 
        />

        <!-- TODO: opciones -->
        <PokemonOptions 
            :pokemons="pokemonArr" 
            @selection-pokemon="checkAnswer($event)" 
        />

        <div v-if="showAnswer">
            <h2 class="fade-in">{{ message }}</h2>
            <button @click="newGame">
                Nuevo Juego
            </button>
        </div>
        
    </div>

</template>

<script>
import PokemonPicture from '@/components/PokemonPicture'
import PokemonOptions from '@/components/PokemonOptions'

import getPokemonOptions from '../helpers/getPokemonOptions'


export default {
    components: { PokemonPicture, PokemonOptions },

    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: ''
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor( Math.random() * 4 )
            this.pokemon = this.pokemonArr[ rndInt ]
        },
        checkAnswer( pokemonId ) {

            this.showPokemon = true
            this.showAnswer = true

            let message = `Oops, era  ${ this.pokemon.name }`

            if(pokemonId == this.pokemon.id) {
                message = `Correcto, ${ this.pokemon.name }`
            }
            this.message = message  
        },
        newGame() {
            this.showPokemon = false,
            this.showAnswer = false,
            this.pokemonArr = [],
            this.pokemon = null,
            this.mixPokemonArray()
        }
    },
    mounted() {
        this.mixPokemonArray()
    }
}
</script>

