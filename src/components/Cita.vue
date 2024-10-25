<template>
  <li
    :style="{ backgroundColor: colorGravedad, color: textColorGravedad }"
    class="card"
  >
    <p><strong>Paciente:</strong> {{ cita.paciente }}</p>
    <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
    <p><strong>Hora:</strong> {{ cita.hora }}</p>
    <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
    <p><strong>Gravedad:</strong> {{ cita.gravedad }}</p>
    <button @click="$emit('eliminar')">Eliminar</button>
  </li>
</template>

<script>
export default {
  props: ["cita"],
  computed: {
    // Determina el color de fondo según la gravedad de la cita
    colorGravedad() {
      switch (this.cita.gravedad) {
        case "Baja":
          return "green";
        case "Media":
          return "yellow";
        case "Alta":
          return "red";
        default:
          return "white";
      }
    },
    // Cambia el color del texto a negro para citas de gravedad media
    textColorGravedad() {
      return this.cita.gravedad === "Media" ? "black" : "white";
    },
  },
};
</script>

<style scoped>
.card {
  width: 300px;
  padding: 1rem;
  margin-bottom: 1rem;
  border-radius: 8px;
  color: #fff;
}
</style>
