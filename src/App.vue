<template>
  <div id="app">
    Ejemplo peticiones AJAX con Axios
    <button id="btn" class="" v-on:click="cargaJson">Cargar Bromas</button>
  
     <!-- Maquetar resultado de la petición AJAX -->
     <div v-for="dato in contenidoJson" :key="dato.id">         
            <div>
              <h3>{{ dato.id }}</h3>
              <p>{{ dato.joke }}</p>
            </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  components: {
  }, 
  data () {
    return {
      contenidoJson: []
    }
  }, 
  methods: {
    cargaJson: function () {
      this.loading = true;
      axios.get("http://api.icndb.com/jokes/random/10")
      .then((response)  =>  {
        this.loading = false;
        this.contenidoJson = response.data.value;
      }, (error)  =>  {
        console.log("Error en peticion AJAX =>"+error)
      })
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
</style>
