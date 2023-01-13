<template>
    <h1>Pokemon Option</h1>
    <ul>
        <li 
            v-for="pokemon in pokemons" 
            :key="pokemon.id"
            @click="$emit('selection-pokemon', pokemon.id)"
        >
            {{ pokemon.name }}
        </li>
        
    </ul>
</template>

<script>
    export default {
        props:{
            pokemons: {
                type: Array,
                required: true,
            }
        }
    }
</script>

<style scoped>
/* Pokemon Options */
ul {
    margin: auto;
    list-style-type: none;
}
li {
    background-color: rgba(0, 0, 0, 0.818);
    color: white;
    padding: .5rem 2rem;
    border-radius: 5px;
    border: none;
    cursor: pointer;
    margin: 10px auto;
    width: 250px;
    border-radius: .5rem;
    transition: all .3s ease-in-out;
}

li:hover {
    transform: scale(1.05);
}

.options-container {
    display: flex;
    justify-content: center;
}

</style>