<template>
    <div class="options-container">

        <ul>
            <!-- En algunas ocasiones hay que colocar el id del pokemon como key -->
            <!-- 
                $emit es para emitir eventos que pueden ser accedidos como si fueran de vue ,
                reciben entre comillas el nombre del evento y despues, si es necesario, argumentos
            -->
            <li v-for="pokemon in pokemons" :key="pokemon.id" @click="$emit( 'selection', pokemon.id )">
                {{ pokemon.name }}
            </li>
        </ul>
        
    </div>
</template>

<script>
export default {
    props: {
        pokemons: {
            type: Array,
            required: true
        }
    },
    name: 'PokemonOptions'
}
</script>

<style scoped>

    ul {
        list-style-type: none;
    }
    li {
        background-color: #fff;
        border-radius: 5px;
        border: 1px solid rgba(0, 0, 0, 0.2);
        cursor: pointer;
        margin-bottom: 10px;
        width: 250px;
    }
    li:hover {
        background-color: rgba(0, 0, 0, 0.05);
    }
    .options-container {
        display: flex;
        justify-content: center;
    }

</style>