<template>
    <h1 v-if="!pokemon">Cargando...</h1>
        

    <div v-else>
        <h1>Quien es este Pokemon</h1>
        
        <PokemonPicture :pokemonId="pokemon?.id" :showPokemon="showPokemon"/>
        <PokemonOption :pokemons="pokemonArr" @selection-pokemon="checkAnswer( $event )"/>

        <template v-if="showAnswer">

            <h2 class="fade-in">{{ message }}</h2>
            <button @click="newGame">Nuevo Juego</button>
        </template>

    </div>

</template>

<script>
    import PokemonPicture from '@/components/PokemonPicture.vue'
    import PokemonOption from '@/components/PokemonOption.vue'
    import getPokemonOptions from '@/helpers/getPokemonOption'

    export default {
        components:{
            PokemonOption,
            PokemonPicture
        },
        data(){
            return{
                pokemonArr: [],
                pokemon: null,
                showPokemon: false,
                showAnswer: false,
                message:''
            }
        },

        methods: {
            async mixPokemonArray(){

                getPokemonOptions();
                this.pokemonArr = await getPokemonOptions()

                const rndInt = Math.floor( Math.random() * 4 )
                this.pokemon = this.pokemonArr[rndInt]
            },

            checkAnswer( pokemonId ){
                this.showPokemon = true
                this.showAnswer = true

                if( pokemonId === this.pokemon.id ){
                    this.message = `Correcto! si es ${ this.pokemon.name }`
                }else{
                    this.message = `Ups! era ${ this.pokemon.name }`
                }
                
            },
            async newGame(){
                this.showPokemon = false
                this.showAnswer = false
                this.pokemon = null
                await this.mixPokemonArray()
            }
        },

        mounted(){
            this.mixPokemonArray()
        }
    }
</script>

<style>
button{
    background-color: white;
cursor: pointer;
    border: none;
    color: black;
    border-radius: .25rem;
    padding: .5rem 2rem;
}
</style>