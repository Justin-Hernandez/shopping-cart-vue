<template>
  <div class="card border-0">
    <div class="card-header py-0 border-0 fs-6">
      <div class="row">
        <div class="col-12 col-sm-6 col-lg-9 p-0 px-2 text-truncate h6">
          {{ codigo }}
        </div>
        <div
          class="col-12 col-sm-6 col-lg-3 stock text-center text-truncate h6"
        >
          {{ stock }}
        </div>
      </div>
    </div>

    <img
      v-bind:src="imgURL"
      v-bind:alt="codigo"
      v-bind:class="opacity"
      class="card-img-top rounded-2"
      @mouseenter="ampliarImagen"
      @mouseleave="resetearImagen"
    />

    <div class="card-body text-center">
      <h5 class="card-title text-truncate">{{ precio }}€</h5>
      <p class="card-text">{{ descripcion }}</p>
    </div>

    <div class="card-footer border-0 p-2">
      <button
        type="button"
        class="btn btn-outline-dark btn-add w-100 border-0"
        v-bind:disabled="disabled"
        @click="insertarItemCarrito"
      >
        Añadir
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ItemCard",
  props: {
    codigo: String,
    stock: Number,
    descripcion: String,
    precio: Number,
    img: String,
    columna: Number,
    categoria: String
  },
  computed: {
    imgURL: function () {
      // si se ha generado con URL.createObjectURL()
      // al insertar un nuevo Item no hace falta hacer require()
      return !this.img.includes("blob")
        ? require(`../../../src/assets/${this.img}`)
        : this.img;
    },
    opacity: function() {return this.stock <= 0 ? 'opacity-50' : 'opacity-100'},
    disabled: function() { return this.stock <= 0}
  },
  methods: {
    ampliarImagen: function (event) {
      event.target.style["z-index"] = "99";
      event.target.style["transition"] = ".2s";
      event.target.style["transform"] = "scale(1.35)";
      event.target.style["box-shadow"] =
        "rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px";

      //si es el ultimo item de la columna, amplia de derecha a izquierda
      //si es el primer item de la columna, amplia de iquierda a derecha
      //si es un item del centro amplia en el centro
      if (this.columna % 4 === 0) {
        event.target.style["transform-origin"] = "100% 0%";
      } else if (this.columna % 4 === 1) {
        event.target.style["transform-origin"] = "0% 0%";
      } else {
        event.target.style["transform-origin"] = "50% 0%";
      }
    },
    resetearImagen: function (event) {
      event.target.style["z-index"] = "1";
      event.target.style["transition"] = ".2s";
      event.target.style["transform"] = "scale(1)";
      event.target.style["box-shadow"] = "";
    },
    insertarItemCarrito: function() {
      this.$emit("insertar-item-carrito", this.categoria, {...this.$props})
    }
  },
};
</script>

<style scoped>
.card,
.btn {
  background-color: white;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.card .card-text {
  overflow-y: scroll;
  min-height: 60px;
  max-height: 60px;
}

.card .card-header,
.card .card-footer {
  background-color: white;
}
</style>