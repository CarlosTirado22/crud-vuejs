<template>
  <div class="contenedor">
    <h1>Practica CRUD</h1>
    <div class="cardO">
      <div class="card1">
        <button v-on:click="openModalAgg(index)" class="actu btn btn-primary">Agregar</button>

        <div class="resul">
          <table class="table">
            <thead>
              <tr>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>Teléfono</th>
                <th>Acciones</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(tarea, index) in arrayTareas" :key="index">
                <td>{{ tarea.nombre }}</td>
                <td>{{ tarea.apellido }}</td>
                <td>{{ tarea.telefono }}</td>
                <td>
                  <button v-on:click="openModal(index)" class="editar"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#000000" stroke-width="1" stroke-linecap="round" stroke-linejoin="round"><path d="M20 14.66V20a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h5.34"></path><polygon points="18 2 22 6 12 16 8 16 8 12 18 2"></polygon></svg></button>
                  <button v-on:click="resetear(index)" class="borrar"><svg  width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#000000"  ><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path><line x1="10" y1="11" x2="10" y2="17"></line><line x1="14" y1="11" x2="14" y2="17"></line></svg></button>
                </td>
              </tr>
            </tbody>
          </table>
          
        </div>
        <!-- <Tabla /> -->
        

        <!-- Modal para agregar -->
        <div v-if="modalVisibleAgg" class="modal">
          <div class="modal-content">
            <span v-on:click="closeModal" class="close">&times;</span>
            <input v-model="nombre" type="text" class="form-control input textactua " placeholder="Nombre">
            <input v-model="apellido" type="text" class="form-control input textactua " placeholder="Apellido">
            <input v-model="telefono" type="number" class="form-control input textactua " placeholder="Telefono">
            <button v-on:click="add" class="btn btn-outline-primary actualizar" type="button">Agregar</button>
          </div>
        </div>
        <!--Fin Modal para agregar -->

        <!-- Modal de edición -->
        <div v-if="modalVisible" class="modal">
          <div class="modal-content">
            <span v-on:click="closeModal" class="close">&times;</span>
            <input v-model="nombreActu" type="text" class="form-control input textactua " placeholder="Nombre">
            <input v-model="apellidoActu" type="text" class="form-control input textactua " placeholder="Apellido">
            <input v-model="telefonoActu" type="number" class="form-control input textactua " placeholder="Telefono">
            <button v-on:click="actualizar(indexSeleccionado)" class="btn btn-outline-primary actualizar" type="button">Actualizar</button>
          </div>
        </div>
        
      </div>
    </div>
  </div>
  
</template>

<script setup>
// import Tabla from './Tabla.vue'
import { ref } from 'vue';

const nombre = ref(""); 
const apellido = ref(""); 
const telefono = ref(null); 
const arrayTareas = ref([]);
const nombreActu = ref(""); 
const apellidoActu = ref(""); 
const telefonoActu = ref(null);
const indexSeleccionado = ref(null); 
const modalVisible = ref(false);
const modalVisibleAgg = ref(false);

const add = () => {
  if (nombre.value.trim() !== "" && apellido.value.trim() !== "" && telefono.value !== null) {
    arrayTareas.value.push({ 
      nombre: nombre.value,  
      apellido: apellido.value, 
      telefono: parseInt(telefono.value) // Convertir a número
    });
    nombre.value = "";
    apellido.value = "";
    telefono.value = null; // Reiniciar el valor a null
    closeModal();
  }
};

const resetear = (index) => {
  arrayTareas.value.splice(index, 1);
};

const openModal = (index) => {
  modalVisible.value = true;
  nombreActu.value = arrayTareas.value[index].nombre;
  apellidoActu.value = arrayTareas.value[index].apellido;
  telefonoActu.value = arrayTareas.value[index].telefono;
  indexSeleccionado.value = index;
};

const openModalAgg = (index) => {
  modalVisibleAgg.value = true;
  indexSeleccionado.value = index;
};

const closeModal = () => {
  modalVisible.value = false;
  modalVisibleAgg.value = false;
  textoActualizacion.value = "";
  indexSeleccionado.value = null;
};


const actualizar = (index) => {
  if (nombreActu.value.trim() !== "" && index !== null && apellidoActu.value.trim() !== "" && telefonoActu.value !== null) {
    arrayTareas.value[index].nombre = nombreActu.value;
    arrayTareas.value[index].apellido = apellidoActu.value;
    arrayTareas.value[index].telefono = parseInt(telefonoActu.value); // Convertir a número
    closeModal();
  }
};
</script>

<style>

.contenedor{
  background: #F8F9FA;
  margin: 20px;
  padding: 10px;
  border-radius: 8px;
  box-shadow: 3px 4px 9px rgba(0,0,0,.6);
}

h1{
  margin: 10px;
  margin-top: -5px;
  padding: 5px;
}

.cardO{
  margin: 10px;
  padding: 15px;
  width: 97%;
  display: flex;
  justify-content: center;
}

.card1{
  padding: 15px;
  margin: 20px;
  width: 90%;
  word-break: break-all;
  background-color: #F5F3F4;
  border: 1px solid #ccc;
  box-shadow: 1px 1px 6px rgba(0,0,0);
}

.resul{
  margin: 10px;
  background: #EDEDE9;
  justify-content: space-between;
  display: flex;
  border: 1px solid #ccc;
  box-shadow: 1px 1px 6px rgb(142, 165, 165);
}

span{
  margin: 10px;
}

.borrar{
  margin: 5px;
  border: none;
}

.boton{
  border: none;
  border-radius: 10px;
  font-size: 18px;
}


/* Estilos para el modal */
.modal {
  display: block;
  position: fixed; 
  z-index: 1; 
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto; 
  background-color: rgb(0,0,0);
  background-color: rgba(0,0,0,0.4); 
}

.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  margin-top: 9%;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
  margin-left: 97%;
  margin-top: -10px;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.actualizar{
  width:  10%;
  padding: 10px;
  margin: 10px auto;
}

.actu{
  margin: 10px;
  margin-left: -.1px;
}

.textactua{
  width: 40%;
  margin: 10px auto;
}

.editar{
  border: none;
  vertical-align: auto;
  font-family: 'Raleway', sans-serif;
  font-size: 16px;
  letter-spacing: .07em;
}


/* PARA DISPOSITIVOS MOVILES */
@media (max-width: 768px){
.contenedor{
  margin: 25px;
  height: 100%;
  margin-top: 20%;
}

.card1{
  max-width: 100%;
}

.footer{
  margin-right: 40%;
}

}
</style>
