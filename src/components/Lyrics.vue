<template>
  <h1 class="mt-5">Letra de Canciones</h1>

  <div class="container">
    <div class="row">
      <div class="col-md-4">
        <form @submit.prevent="funcion">
          <div class="mb-3">
            <label for="artista" class="form-label">Artista</label>
            <input type="text" class="form-control" v-model="artist" required>
          </div>
          <div class="mb-3">
            <label for="cancion" class="form-label">Canción</label>
            <input type="text" class="form-control" v-model="lyrics" required>
          </div>
          <div class="d-grip gap-2">
            <button  class="btn btn-success">Buscar</button>
          </div>
        </form>
      </div>
      <div class="result col-md-8">
        <h2 class="text-center mb-2">{{artista}}</h2>
        <div class="mt-4">{{cancion}}</div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      artista: "",
      cancion: "",
    };
  },
  methods: {
    async submit() {
      console.log('Se ejecuta métdoo submit');
      const letraCancion = await consumirCanciones(this.artista, this.cancion);
      console.log(letraCancion);
    }
  }
}
</script>

<style>

</style>