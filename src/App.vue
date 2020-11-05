<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <main class="app-container">
    <div class="form-usuario">
      <input type="text" placeholder="Nombre" v-model="nombre"/>
      <input type="text" placeholder="Apellido" v-model="apellido"/>
      <button @click="agregarUsario" type="button">Agregar</button>
    </div>
    <div class="nombreActual" v-if="nombreCompleto !== ' '">
      {{ nombreCompleto }}
    </div>
    <ListadoUsuarios msg="Listado de usuarios" :usuarios="listadoDeUsuarios" @eliminar-usuario="eliminarUsuario"/>
  </main>
</template>

<script>
import { onMounted } from 'vue';
// import { computed, reactive, ref, watch } from 'vue'
import ListadoUsuarios from './components/ListadoUsuarios.vue'

export default {
  name: 'App',
  components: {
    ListadoUsuarios
  },
  setup() {
    const usuario = reactive({
      nombre: 'Nicolas',
      apellido: 'Priano'      
    })

    const listadoDeUsuarios = ref([]);

    const nombreCompleto = computed(() => `${usuario.nombre} ${usuario.apellido}`);

    const agregarUsuario = () => {
      listadoDeUsuarios.value = [...listadoDeUsuarios.value, { nombre: usuario.nombre, apellido: usuario.apellido }];
      usuario.nombre = '';
      usuario.apellido = '';
    }

    const eliminarUsuario = usuario => {
      listadoDeUsuarios.value = listadoDeUsuarios.value.filter(usr => usr.nombre !== usuario.nombre || usr.apellido !== usuario.apellido);
    }

    watch(listadoDeUsuarios, (currListadoDeUsuarios, prevListadoDeUsuarios) => {
      if(currListadoDeUsuarios.length > prevListadoDeUsuarios.length) {
        console.log(`Se agrego un usuario (${currListadoDeUsuarios.length} > ${prevListadoDeUsuarios.length})`);
      } else {
        console.log(`Se elimino un usuario (${currListadoDeUsuarios.length} < ${prevListadoDeUsuarios.length})`);
      }
    })

    onMounted(() => {
      console.log('Mounted!')
    })

    return {
      usuario,
      nombreCompleto,
      agregarUsuario,
      eliminarUsuario,
      listadoDeUsuarios
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.nombreActual {
  background-color: beige;
  border-radius: 5px;
  margin: 10px;
  padding: 15px;
  width: 250px;
}

.app-container {
  display: flex;
  flex-flow: column wrap;
  justify-content: center;
  align-items: center;
}

.form-usuario {
  display: flex;
  flex-flow: row wrap;
}
.form-usuario input {
  border: 1px solid #cccccc;
  border-radius: 5px;
  font-size: 14px;
  margin: 10px;
  padding: 10px;
}

.form-usuario button {
  border-radius: 5px;
  margin: 10px;
  padding: 10px;
}
</style>
