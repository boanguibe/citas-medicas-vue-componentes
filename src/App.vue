<template>
  <div>
    <!-- Formulario para agregar una nueva cita médica -->
    <form @submit.prevent="agregarCita">
      <label :style="{ color: nuevoCita.paciente ? 'white' : 'red' }"
        >Paciente:
      </label>
      <input v-model="nuevoCita.paciente" placeholder="Nombre del paciente" />

      <label :style="{ color: nuevoCita.fecha ? 'white' : 'red' }"
        >Fecha:
      </label>
      <input v-model="nuevoCita.fecha" type="date" />

      <label :style="{ color: nuevoCita.hora ? 'white' : 'red' }">Hora: </label>
      <input v-model="nuevoCita.hora" type="time" />

      <label :style="{ color: nuevoCita.gravedad ? 'white' : 'red' }"
        >Gravedad:
      </label>
      <select v-model="nuevoCita.gravedad">
        <option disabled value="">Selecciona la gravedad</option>
        <option value="Baja">Baja</option>
        <option value="Media">Media</option>
        <option value="Alta">Alta</option>
      </select>

      <label :style="{ color: nuevoCita.motivo ? 'black' : 'red' }"
        >Motivo:</label
      >
      <input v-model="nuevoCita.motivo" placeholder="Motivo de la consulta" />

      <button type="submit" :disabled="!camposCompletos">Agregar Cita</button>
    </form>

    <!-- Mostrar mensaje si no hay citas registradas -->
    <p v-if="citas.length === 0" class="texto">No hay citas registradas aún.</p>

    <!-- Lista de citas, con grid para organizar en filas de tres elementos -->
    <ul v-else class="citas-grid">
      <Cita
        v-for="(cita, index) in citas"
        :key="index"
        :cita="cita"
        @eliminar="eliminarCita(index)"
      />
    </ul>
  </div>
</template>

<script>
import Cita from "./components/Cita.vue";

export default {
  components: { Cita },
  data() {
    return {
      nuevoCita: {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      },
      citas: [],
    };
  },
  computed: {
    camposCompletos() {
      return (
        this.nuevoCita.paciente &&
        this.nuevoCita.fecha &&
        this.nuevoCita.hora &&
        this.nuevoCita.gravedad &&
        this.nuevoCita.motivo
      );
    },
  },
  methods: {
    agregarCita() {
      if (this.camposCompletos) {
        this.citas.push({ ...this.nuevoCita });
        this.limpiarFormulario();
      }
    },
    limpiarFormulario() {
      this.nuevoCita = {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      };
    },
    eliminarCita(index) {
      this.citas.splice(index, 1);
    },
  },
};
</script>

<style scoped>
ul.citas-grid {
  display: grid;
  grid-template-columns: repeat(
    3,
    1fr
  ); /* Organiza las citas en filas de tres columnas */
  gap: 1rem;
  list-style-type: none;
  padding: 0;
}
.texto {
  color: red;
}
</style>
