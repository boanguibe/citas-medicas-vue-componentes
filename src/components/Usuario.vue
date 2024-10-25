<template>
    <!-- Cada usuario está representado dentro de un elemento <li> -->
    <li>
      <!-- Muestra el nombre y el email del usuario, y permite hacer clic para mostrar el detalle del usuario -->
      <p @click="mostrarDetalle">{{ usuario.nombre }} - {{ usuario.email }}</p>
      
      <!-- Muestra la foto del usuario, y al hacer clic en la imagen también se muestra el detalle del usuario -->
      <img :src="usuario.url" alt="Foto del usuario" width="50" @click="mostrarDetalle">
      
      <!-- Botón para eliminar al usuario, emite el evento personalizado 'eliminar' hacia el componente padre -->
      <button @click="$emit('eliminar')">Eliminar</button>
    </li>
  </template>
  
  <script>
  export default {
    // Propiedad que recibe el objeto 'usuario' desde el componente padre
    props: ['usuario'],
    
    methods: {
      // Método que emite un evento personalizado 'mostrarDetalle' al componente padre,
      // pasando el objeto 'usuario' como argumento
      mostrarDetalle() {
        this.$emit('mostrarDetalle', this.usuario);
      }
    }
  };
  </script>
  
  <style>
  /* No se necesita estilo adicional por el momento */
  </style>
  