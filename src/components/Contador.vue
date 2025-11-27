<template>
  <div>
    
    <h1>{{ tit }}</h1>

    <p>{{ numero }} <sup>2</sup> = {{ calculaCuadrado}}</p>
    <p>{{ numero }} <sup>2</sup> = {{ calculaCuadrado}}</p>
    <p>{{ numero }} <sup>2</sup> = {{ calculaCuadrado}}</p>
    <p>{{ numero }} <sup>2</sup> = {{ calculaCubo }}</p>
    <p>{{ numero }} <sup>2</sup> = {{ obtenerCubo()}}</p>
    
    <div>
      <button @:click="incrementar()">+1</button>
      <button @:click="decrementar()">-1</button>
      <button v-show="mostrar">prueba</button>
    </div>
  </div>
</template>

<script>

// Variable llamada numero inicializada en 10, {{}} para usar javascript
export default {
  data(){
    return {
      numero: this.inicio,
      titulo: "Contador"
    };
  },
  methods: {
    obtenerCuadrado(){
      console.log("Entro a obtener cuadrado");
      return this.numero * this.numero; // cuando usamos una propiedad reactiva debemos usar this
    },
    obtenerCubo(){
      return this.numero * this.numero * this.numero;
    },

    incrementar(){
      console.log(this.tit)
      this.numero ++;
    },
    decrementar(){
      this.numero --;
    },
    
  },
  computed:{
    calculaCuadrado(){
      console.log("Entro a propiedad computada");
      return this.numero * this.numero;
    },

    calculaCubo(){
      console.log("Entro a propiedad computada");
      return this.numero * this.numero * this.numero;
    },

  },
 /*props:["tit","inicio","mostrar"],declaracion basica de props*/
 props:{
  tit: String,
  inicio: {
    type: Number,
    default: 99,
    validator(value){
      return value >10;
    }
  },
  mostrar: Boolean
 }
 /* String, Number, Boolean, Array, Object, Date, Function, BigInt*/ 
};
</script>

<style>

</style>