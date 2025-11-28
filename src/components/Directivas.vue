<template>
<div>
    <label for="id_nombre">Nombre</label>
    <input v-model="nombre" id="id_nombre" type="text">
    <p>{{ nombre }}</p>
    

    <label for="id_apellido">Apellido</label>
    <input v-model="apellido" id="id_apellido" type="text">

    <button v-on:click="imprimirNombre()">  Imprimir Nombre</button>
    <button v-on:click="agregarEstudiante()"> Agregar Estudiante</button>
    
    <h1>{{ arreglo[0] }}</h1>

    <ul>
        <li 
        v-show="nombre" 
        v-for="{nombre,apellido} in arreglo" 
        :key="nombre"
        >
            {{ nombre }} - {{ apellido }}
        </li>
      
    </ul>

    <h2>Tabla</h2>

    <table border="1">
        <thead>
        <tr>
            <th>Nombre</th>
            <th>Apellido</th>
        </tr>
    </thead>
     <!--Al usar v-for con desestructuracion de datos siempre usar el nombre de las variables del objeto y no poner otras nombres-->
    <tbody>
        <tr v-for="{nombre,apellido} in arreglo" :key="nombre">

            <th>{{ nombre }}</th>
            <th>{{ apellido }}</th>
        </tr>
        
       

    </tbody>

    </table>
    


</div>
</template>

<script>
export default {
  data() {
    return {
        nombre: null,
        apellido: null,
        /* arreglo[1,2,3,4] */
        arreglo:[],
        

    };
  },
  methods: {
    imprimirNombre(){
        console.log(this.nombre);
    },
    agregarEstudiante(){
        const estu={
            nombre:this.nombre,
            apellido:this.apellido

        };
        console.log("se agrega estudiante");
        console.log(estu);
        this.arreglo.push(estu);
        this.limpiarFormulario();
    },
    limpiarFormulario(){
        this.nombre=null;
        this.apellido=null;
    }

  },
};
</script>

<style>
</style>
