<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <main class="app-container">
    <form class="form-carrito">
      <input type="text" placeholder="Nombre del producto"/>
      <button type="submit" disabled="true">Agregar</button>
    </form>
    <div class="card-nombre">
     Nombre del producto va aca
    </div>
    <ListadoUsuarios/>
  </main>
</template>

<script>
import ListadoUsuarios from './components/ListadoProductos.vue'

export default {
  name: 'App',
  components: {
    ListadoUsuarios
  },
  data() {
    return  {
      
    }
  },
  methods: {

  },
  computed: {
    
  },
  watch: {
    
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

.card-nombre {
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

.form-carrito {
  display: flex;
  flex-flow: row wrap;
}
.form-carrito input {
  border: 1px solid #cccccc;
  border-radius: 5px;
  font-size: 14px;
  margin: 10px;
  padding: 10px;
}

.form-carrito button {
  border-radius: 5px;
  margin: 10px;
  padding: 10px;
}
</style>
