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
// import { computed, reactive, ref, watch } from 'vue'
import ListadoUsuarios from './components/ListadoUsuarios.vue'

export default {
  name: 'App',
  components: {
    ListadoUsuarios
  },
  // setup() {
  //   const usuario = reactive({
  //     nombre: 'Nicolas',
  //     apellido: 'Priano'      
  //   })

  //   const listadoDeUsuarios = ref([]);

  //   const nombreCompleto = computed(() => `${usuario.nombre} ${usuario.apellido}`);

  //   const agregarUsuario = () => {
  //     listadoDeUsuarios.value = [...listadoDeUsuarios.value, { nombre: usuario.nombre, apellido: usuario.apellido }];
  //     usuario.nombre = '';
  //     usuario.apellido = '';
  //   }

  //   const eliminarUsuario = usuario => {
  //     listadoDeUsuarios.value = listadoDeUsuarios.value.filter(usr => usr.nombre !== usuario.nombre || usr.apellido !== usuario.apellido);
  //   }

  //   watch(listadoDeUsuarios, (currListadoDeUsuarios, prevListadoDeUsuarios) => {
  //     if(currListadoDeUsuarios.length > prevListadoDeUsuarios.length) {
  //       console.log(`Se agrego un usuario (${currListadoDeUsuarios.length} > ${prevListadoDeUsuarios.length})`);
  //     } else {
  //       console.log(`Se elimino un usuario (${currListadoDeUsuarios.length} < ${prevListadoDeUsuarios.length})`);
  //     }
  //   })

  //   return {
  //     usuario,
  //     nombreCompleto,
  //     agregarUsuario,
  //     eliminarUsuario,
  //     listadoDeUsuarios
  //   }
  // },
  // options API
  data() {
    return  {
      nombre: 'Nicolas',
      apellido: 'Priano',
      listadoDeUsuarios: []
    }
  },
  methods: {
    agregarUsuario() {
      console.log('clicked')
      this.listadoDeUsuarios.push({
        nombre: this.nombre,
        apellido: this.apellido
      });
      this.nombre = ''
      this.apellido = ''
    },
    eliminarUsuario() {
      this.listadoDeUsuarios = this.listadoDeUsuarios.filter(usr => usr.nombre !== this.nombre || usr.apellido !== this.apellido);
    }
  },
  computed: {
    nombreCompleto: function () {
      return `${this.nombre} ${this.apellido}`
    },
  },
  watch: {
    listadoDeUsuarios (currListadoDeUsuarios) {
      if(currListadoDeUsuarios.length > this.listadoDeUsuarios.length) {
        console.log(`Se agrego un usuario (${this.listadoDeUsuarios.length} > ${this.listadoDeUsuarios.length})`);
      } else {
        console.log(`Se elimino un usuario (${this.listadoDeUsuarios.length} < ${this.listadoDeUsuarios.length})`);
      }
    }
  },
  created() {
    
  },
  mounted() {

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
