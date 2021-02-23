<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <main class="app-container">
    <form class="form-usuario" @submit.prevent="agregarUsuario">
      <input type="text" placeholder="Nombre" v-model="usuario.nombre" ref="nombre"/>
      <input type="text" placeholder="Apellido" v-model="usuario.apellido" ref="apellido"/>
      <button type="submit">Agregar</button>
    </form>
    <div class="nombreActual" v-if="nombreCompleto !== ' '">
      {{ nombreCompleto }}
    </div>
    <ListadoUsuarios msg="Listado de usuarios" :usuarios="listadoDeUsuarios" @eliminar-usuario="eliminarUsuario"/>
  </main>
</template>

<script>
import ListadoUsuarios from './components/ListadoUsuarios.vue'

export default {
  name: 'App',
  components: {
    ListadoUsuarios
  },
  data() {
    return  {
      usuario: {
        nombre: 'Pepe',
        apellido: 'Sanchez',
      },
      listadoDeUsuarios: []
    }
  },
  methods: {
    agregarUsuario() {
      this.listadoDeUsuarios.push({
        nombre: this.usuario.nombre,
        apellido: this.usuario.apellido
      });
      this.usuario.nombre = ''
      this.usuario.apellido = ''

      this.$refs.nombre.focus();
    },
    eliminarUsuario(usuario) {
      this.listadoDeUsuarios = this.listadoDeUsuarios.filter(usr => usr.nombre !== usuario.nombre || usr.apellido !== usuario.apellido);
    }
  },
  computed: {
    nombreCompleto: function () {
      return `${this.usuario.nombre} ${this.usuario.apellido}`
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
    console.log('Created!')
  },
  mounted() {
    console.log('Mounted!')
  },
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
