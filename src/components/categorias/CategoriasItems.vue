<template>
  <div class="row">
    <div class="col-12" v-for="(value, name) in items" v-bind:key="name">
      <CategoriaItems
        v-bind:categoria="name"
        v-bind:items="value"
        v-on:insertar-nuevo-item="insertarNuevoItem"
        v-on:insertar-item-carrito="insertarItemCarrito"
      />
    </div>

    <div class="col-12">
      <NuevaCategoria v-on:insertar-categoria="insertarCategoria" />
    </div>
  </div>
</template>

<script>
import CategoriaItems from "./CategoriaItems.vue";
import NuevaCategoria from "./NuevaCategoria.vue";

export default {
  name: "CategoriasItems",
  props: {
    items: Object,
  },
  components: {
    CategoriaItems,
    NuevaCategoria,
  },
  methods: {
    // captura el evento emitido en nuevaCategoria y lo propaga al padre
    // que es donde se modifica el estado del componente y se añade la nueva categoria
    insertarCategoria: function (nombre) {
      this.$emit("insertar-categoria", nombre);
    },
    insertarNuevoItem: function (categoria, nuevoItem) {
      this.$emit("insertar-nuevo-item", categoria, nuevoItem);
    },
    insertarItemCarrito: function (categoria, item) {
      this.$emit("insertar-item-carrito", categoria, item);
    }
  },
};
</script>

<style scoped>
</style>