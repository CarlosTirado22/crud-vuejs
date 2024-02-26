<script setup>

</script>

<template>

  <main>
    <table class="table table-hover">
        <thead>
            <tr>
                <th scope="col">Nombre</th>
                <th scope="col">Apellido</th>
                <th scope="col">Telefono</th>
                <th scope="col">Acciones</th>
            </tr>
        </thead>
        <tbody >
            <tr v-for="(tarea, index) in arrayTareas" :key="index">
                <td>{{ tarea.nombre }}</td>
                <td>{{ tarea.apellido }}</td>
                <td>{{ tarea.telefono }}</td>
                <td>
                  <button v-on:click="openModal(index)" class="editar">Editar</button>
                  <button v-on:click="resetear(index)" class="borrar">Borrar</button>
                </td>
            </tr>
        </tbody>
    </table>
  </main>
</template>

<style scoped>

</style>
