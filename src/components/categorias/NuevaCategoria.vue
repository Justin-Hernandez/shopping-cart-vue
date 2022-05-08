<template>
  <div
    v-if="!mostrarForm"
    class="btn w-100 mb-1 border-0 btn-outline-dark"
    @click="alternarForm"
  >
    + Nueva Categoria +
  </div>
  <div v-else>
    <form @submit.prevent="insertarCategoria">
      <div class="d-flex justify-content-center w-100">
        <input
          v-model="nombreCategoria"
          type="text"
          class="text-center input-sm border-0 w-75 rounded-2 me-1"
          name="categoria"
          maxLength="15"
          required
        />
        <button type="submit" class="btn btn-outline-dark border-0 w-25 me-1">
          Crear
        </button>
        <button
          type="button"
          class="btn btn-outline-danger btn-cancelar border-0 w-25"
          @click="alternarForm"
        >
          Cancelar
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "NuevaCategoria",
  data() {
    return {
      mostrarForm: false,
      nombreCategoria: ""
    };
  },
  methods: {
    alternarForm: function () {
      this.mostrarForm = !this.mostrarForm;
    },
    insertarCategoria: function () {

      // emite un evento capturado por el padre
      this.$emit("insertar-categoria", this.nombreCategoria)

      // resetea el nombre de la categoria
      this.nombreCategoria = ""
      this.alternarForm()
    },
  },
};
</script>

<style scoped>
.btn,
input {
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.btn-outline-dark {
  background-color: white;
}

.btn-outline-danger {
  background-color: white;
}
</style>