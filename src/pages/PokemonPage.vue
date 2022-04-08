<template>

    <h1 v-if="!pokemon" >Wait...</h1>

    <div v-else>

        <h1>Who is this pokemon?</h1>

        <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />

        <!-- 
            accediendo al $emit selection que se declaro en PokemonOptions y pasandole un method ,
            para acceder a los argumentos del $emit, se necesita usar $event
        -->
        <PokemonOptions v-if="showOptions" :pokemons="pokemonArr" @selection="checkAnswer" />

        <!-- 
            si se desea agregar un agrupador, pero que no sea un div, se puede utilizar
            template, agrupa los elementos y no se muestra en el html 
        -->
        <div v-if="showAnswer">

            <h2 class="fade-in">{{ message }}</h2>
            <button @click="newGame">New Game</button>

        </div>

    </div>


</template>

<script>
import PokemonPicture from '@/components/PokemonPicture'
import PokemonOptions from '@/components/PokemonOptions'
import getPokemonOptions from '@/helpers/getPokemonOptions'

export default {
    name: 'PokemonPage',
    components: {
        PokemonPicture, PokemonOptions
    },
    data(){
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            showOptions: true,
            message: ''
        }
    },
    methods: {
        // ! los methods tambien pueden usar async y await
        async mixPokemonArray(){

            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor( Math.random() * 4 )

            this.pokemon = this.pokemonArr[rndInt]

        },
        checkAnswer( selectedId ){
            
            this.showAnswer = true
            this.showPokemon = true
            this.showOptions = false

            if(selectedId === this.pokemon.id){
                this.message = `Great! ${ this.pokemon.name }`
            }else {
                this.message = `Oops! was ${ this.pokemon.name }`
            }

        },
        newGame(){
            
            this.showPokemon = false
            this.showAnswer = false
            this.showOptions = true
            this.pokemonArr = []
            this.pokemon    = null
            this.mixPokemonArray()

        }
    },
    // ! LIFECYCLE HOOKS
    mounted(){

        this.mixPokemonArray()

    }
}
</script>
