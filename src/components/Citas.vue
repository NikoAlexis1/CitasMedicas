<template>
    <div id="card" :class="{ 'leve': gravedad == 'Leve', 'medio': gravedad == 'Medio', 'grave colorletra': gravedad == 'Grave' }">

        <h3>Paciente</h3>
        <p>{{ paciente }}</p>
        <h3>Fecha</h3>
        <p>{{ fecha }}</p>
        <h3>Hora</h3>
        <p>{{ hora }}</p>
        <h3>Motivo</h3>
        <p>{{ motivo }}</p>
        <button @click="$emit('eliminar')">Eliminar</button>
        
    </div>
</template>

<script>
export default {
    props: { paciente: "", fecha: "", hora: "", motivo: "", gravedad: "" }
}

</script>

<style scoped>
#card {
    width: 200px;
    text-align: center;
    padding-top: 1px;
    border-radius: 5px;
}
button{
    margin-bottom: 20px;
}

.colorletra {
    color: #fff;
}

.leve {
    background-color: #9eda45;
}
.medio {
    background-color: #ffd901;
}
.grave {
    background-color: #dd0000;
}
</style>