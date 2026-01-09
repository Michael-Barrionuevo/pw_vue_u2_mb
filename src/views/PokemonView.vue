<template>
    <div>
        <PokemonImagen :pokemonId="pokemonGanador"/>
        <PokemonOpciones @seleccionado= "evaluarGanador($event)" :listaPokemons="pokemonArr" />

    </div>

    <div v-if="resultado">
        <h1 v-if="resultado === 'ganador'"> Felicidades Ganaste</h1>
        <h1 v-else>Perdiste</h1>

    </div>
  
</template>

<script>
    import PokemonImagen from '../components/PokemonImagen.vue';
    import PokemonOpciones from '../components/PokemonOpciones.vue';
    import { obtenerVectorPokemonFachada, obtenerAleatorioFachada } from '../clients/PokemonClient.js';

export default {
    components: {
        PokemonImagen,
        PokemonOpciones,
    },
    data() {
        return {
            pokemonArr:[],
            pokemonGanador: null,
            resultado: null,
            
        };
    },
    mounted(){
        console.log('componente montado');
        this.iniciarJuego();
    },
    methods:{
        async iniciarJuego(){
            this.pokemonArr = await obtenerVectorPokemonFachada();

            const IdAleatorio = obtenerAleatorioFachada(0,3);
            this.pokemonGanador = this.pokemonArr[IdAleatorio].id;
        },
        evaluarGanador(idGanador){
            console.log('Valor recibido desde padre');
            console.log(idGanador);
            if(idGanador === this.pokemonGanador){
                console.log("Ganador");
                this.resultado = 'ganador';
            }else{
                console.log("Perdedor");
                this.resultado = 'perdedor';
            }

        },
    },

};
</script>

<style>
body{
  background: white;
  color: black;
}

h1{
    text-align: center;
    color: red;
}
</style>