<script>
import Citas from './components/Citas.vue';
export default {
  data() {
    return {
      nivelesGrav: ["Leve", "Medio", "Grave"],
      nuevaCita: {
        paciente: "",
        fecha: "",
        hora: "",
        motivo: "",
        nivelSelec: "",
      },
      citas: [],

    }
  },
  components: {
    Citas,
  },
  methods: {
    agregarCita() {
      this.citas.push({ ...this.nuevaCita });
    },
    eliminarCita(i) {
      this.citas.splice(i, 1);
    },
    limpiar() {
      this.nuevaCita.paciente = "";
      this.nuevaCita.fecha = "";
      this.nuevaCita.hora = "";
      this.nuevaCita.motivo = "";
      this.nuevaCita.nivelSelec = "";
    }
  }
}
</script>

<template>
  <div class="container">

    <!--Formulario-->
    <div class="formulario">
      <form @submit.prevent="agregarCita"@submit="limpiar">
        <div>
          <label :class="{ 'color': nuevaCita.paciente == '' }" for="paciente">Paciente</label>
          <input id="paciente" type="text" v-model="nuevaCita.paciente">
        </div>

        <div>
          <label :class="{ 'color': nuevaCita.fecha == '' }" for="fecha">Fecha</label>
          <input id="fecha" type="date" v-model="nuevaCita.fecha">
        </div>

        <div>
          <label :class="{ 'color': nuevaCita.hora == '' }" for="hora">Hora</label>
          <input id="hora" type="time" v-model="nuevaCita.hora">
        </div>

        <div>
          <label :class="{ 'color': nuevaCita.nivelSelec == '' }" for="gravedad">Gravedad</label>
          <select id="gravedad" v-model="nuevaCita.nivelSelec">
            <option v-for="nivel in nivelesGrav" :value="nivel">{{ nivel }}</option>
          </select>
        </div>

        <div>
          <label :class="{ 'color': nuevaCita.motivo == '' }" for="motivo">Motivo</label>
          <input id="motivo" type="text" v-model="nuevaCita.motivo">
        </div>
        <div class="button">
          <button
            :disabled="nuevaCita.paciente == '' || nuevaCita.fecha == '' || nuevaCita.hora == '' || nuevaCita.gravedad == '' || nuevaCita.motivo == ''">
            Agregar
          </button>
        </div>
      </form>
    </div>


    <!--Informacion de Citas-->
    <div class="informacion">
      <div v-if="citas.length == 0" class="sinCitas">
        <p :class="'color'">Aun no hay consultas registradas</p>
      </div>
      <div v-else v-for="(cita, i) in citas" class="conCitas">
        <Citas :paciente="cita.paciente" :fecha="cita.fecha" :hora="cita.hora" :motivo="cita.motivo"
          :gravedad="cita.nivelSelec" @eliminar="eliminarCita(i)" />
      </div>
    </div>


  </div>


</template>

<style scoped>
.container {
  font-family: sans-serif;
}

/* Estilo Formulario */
.formulario {
  display: flex;
  justify-content: center;
}
form {
  display: grid;
  grid-template-columns: repeat(5, auto);
  justify-content: space-around;
  width: 950px;
  height: auto;
  border: 3px solid lightgray;
  border-radius: 10px;
  padding: 10px;
  font-weight: bold;
}
input,
select {
  width: 100%;
}
form div {
  text-align: center;
}
.button {
  grid-column: 1/6;
  margin-top: 15px;
}
/* Estilo Formulario */

/* Estilo Citas */
.informacion {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}
.sinCitas {
  text-align: center;
  width: 100%;
}
.conCitas {
  margin: 10px;
}
/* Estilo Citas */

.color {
  color: #ff0000;
}
</style>
