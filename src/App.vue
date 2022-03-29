<template>
<div class="fondo">
  <div class="container">
    <h1 class="text-center mb-3">Letras de Canciones</h1>
    <div class="row mt-5">
      <div class="col-4">
        <form @submit.prevent="submit">
          <div class="formulario mb-3">

              <label for="artista" class="form-label fw-bold">Artista</label>
              <input class="form-control" type="text" v-model="artista"/>

              <label for="cancion" class="form-label fw-bold">Canción</label>
              <input class="form-control" type="text" v-model="cancion"/>

          </div>
          <button class="btn btn-info">Buscar</button>
        </form>
      </div>

      <div class="result col-8 text-center">
        <p class="titulo fw-bold">Letra </p>
        <p class="fw-bold letra"><br>{{resultado}}</p>
      </div>

    </div>
  </div>
</div>
</template>

<script>
import { consumirCanciones } from "./api";
export default {
  name: "App",
  components: {},
  data() {
    return {
      artista: "",
      cancion: "",
      resultado: "",
    };
  },
  methods: {
    async submit() {
      try {
        if (this.artista != null || this.cancion != null) {
          this.$swal.fire({
            title: "El artista o canción no existe. ¡Prueba de nuevo!",
            icon: 'warning',
            showClass: {
              popup: "animate__animated animate__fadeInDown",
            },
            hideClass: {
              popup: "animate__animated animate__fadeOutUp",
            },
          });
        }
      } catch (error) {
        throw error;
      }
      const resultado = await consumirCanciones(this.artista, this.cancion);
      this.resultado = resultado.lyrics;
      console.log('Se ejecuta el método submit'); 
      
    },
  },
};
  
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Oleo+Script+Swash+Caps&family=Secular+One&family=Source+Sans+Pro&display=swap');
.fondo {
  background-image: linear-gradient(rgba(255, 255, 255, 0.514), rgba(255, 255, 255, 0.479)), url('assets/fondo.png');
  background-repeat: no-repeat;
  height: 100vh;
  background-size: cover;
  /* PONER IMAGEN DENTRO DE CONTENEDOR */
}

h1{
  color: #fff;
  font-family: 'Oleo Script Swash Caps', cursive;
  font-size: 90px;
  background-color: rgba(0, 0, 0, 0.459);
}

.formulario {
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 20px;
}

button {
  font-family: 'Secular One', sans-serif;
}
.result {
  color: #000;
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 20px;
  position: relative;
  font-size: 20px;
}

.letra {
  white-space: pre-wrap;
  padding: 2rem;
  position: absolut;
}

</style>