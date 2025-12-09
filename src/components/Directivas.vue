<template>
<div>
    <label for="id_nombre">Nombre</label>
    <input v-model="nombre" id="id_nombre" type="text">
    <p>{{ nombre }}</p>
    

    <label for="id_apellido">Apellido</label>
    <input v-model="apellido" id="id_apellido" type="text">

    <button v-on:click="imprimirNombre()">  Imprimir Nombre</button>
    <button v-on:click="agregarEstudiante()"> Agregar Estudiante</button>

    <hr />

    <label for="id_nombre_1">Nombre</label>
    <input v-model="nombre" id="id_nombre_1" type="text" />

    <label for="id_apellido_1">Apellido</label>
    <input
      v-on:keypress.enter="agregarEstudiante1"
      v-model="apellido"
      id="id_apellido_1"
      type="text"
    />
    
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
      <tbody>
        <tr
          v-show="nombre"
          v-for="{ nombre, apellido } in arreglo"
          :key="nombre"
        >
          <td>{{ nombre }}</td>
          <td>{{ apellido }}</td>
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
    agregarEstudiante1(event) {
      console.log("Evento");
      const estu2 = {
        nombre: this.nombre,
        apellido: this.apellido,
      };
      if (event.charCode !== 13) {
        return;
      }
      this.arreglo.push(estu2);
      this.limpiarFormulario();
      console.log("Presionó el ENTER");
      console.log("Se agrega Estudiante 1");
      console.log(event);
      console.log(event.charCode);
      console.log(event.keyCode);
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
