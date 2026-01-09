<template>
    <div>
        <PokemonImagen :pokemonId="pokemonGanador"/>
        <PokemonOpciones @seleccionado= "evaluarGanador($event)" :listaPokemons="pokemonArr" />

    </div>

    <div v-if="resultado">
        <h1 v-if="resultado === 'ganador'"> Felicidades Ganaste</h1>
        <h1 v-else>Perdiste</h1>

    </div>

   <div>
    <button @click="destruir()">Destruir</button>
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
    /*Crea el componente vfor create y create */
    beforeCreate(){
        console.log("beforeCreate : apenas inicia la instancia del componente");

    },
    created(){
        console.log("create: ya se resolvieron data, computed, methods, watch");

    },

    /* Monta el componente : renderiza o visualiza el componente */
    beforeMount(){
        console.log("beforeMount: justo antes del primer render de un elemento html");
    },

    mounted(){
        console.log('componente montado : el componente ya se renderizo');
        this.iniciarJuego();
    },

    /* Actualizacion de un componente */
    beforeUpdate(){
        console.log("beforeUpdate: cuando cambió un data/props y Vue esta por renderizar");
    },

    updated(){
        console.log("updated: cuando ya se actualizo tras el re-renderizacion");
    },

    /* Desmontaje del componente */
    beforeUnmount(){
        console.log("beforeUnmount: justo antes de que el componente se destruya" );
    },

    unmounted(){
        console.log("unmounted: ya fue removido del DOM y destruido");
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
button{
    display: block;
    margin: auto;
    margin-top: 20px;
    width: 100px;
    height: 40px;
    

    
}
</style>