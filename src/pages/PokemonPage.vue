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

        <h2>{{ message }}</h2>
        <button>
            Nuevo Juego
        </button>
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

            let message = `Oops, era  ${ this.pokemon.name }`

            if(pokemonId == this.pokemon.id) {
                message = `Correcto, ${ this.pokemon.name }`
            }
            this.message = message
            
            setTimeout(() => {
                this.showPokemon = false
                this.message = null
                this.pokemon =  null
                this.mixPokemonArray()
            },2000)
            
        }
    },
    mounted() {
        this.mixPokemonArray()
    }
}
</script>

