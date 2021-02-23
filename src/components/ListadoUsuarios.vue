<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <ul v-if="usuarios.length">
      <li class="nombre-usuario" v-for="usuario in usuarios" :key="usuario.apellido" @click="eliminarUsuario(usuario)">{{ usuario.nombre }} {{ usuario.apellido }}</li>
    </ul>
    <div v-else class="alert-sin-usuarios">No hay usuarios</div>
  </div>
</template>

<script>
export default {
  name: 'ListadoUsuarios',
  props: {
    msg: {
      required: true,
      type: String,
    },
    usuarios: Array,
  },
  methods: {
    eliminarUsuario(usuario) {
      this.$emit('eliminar-usuario', usuario)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.alert-sin-usuarios {
  border-radius: 5px;
  background-color: rgba(255, 20, 20, 0.3);
  padding: 15px;
}

ul {
  list-style-type: none;
  padding: 0;
  text-align: center;
}

.nombre-usuario {
  background-color: #41b883;
  border-radius: 5px;
  color: white;
  margin: 10px 0;
  padding: 15px;
}

.nombre-usuario:hover {
  background-color: rgba(255, 20, 20, 0.5);
}
</style>
