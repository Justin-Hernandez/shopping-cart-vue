<template>
  <div
    class="row item-carrito mx-1 my-1 rounded-2"
    @mouseover="visualizarBoton"
    @mouseleave="esconderBoton"
  >
    <div class="col-10 pt-1">
      <h6>{{ codigo }}</h6>
    </div>

    <div class="col-2 p-1" v-bind:class="deleteVisible ? '' : 'invisible'">
      <button
        type="button"
        class="btn btn-danger w-100 p-0"
        @click="eliminarItemCarrito"
      >
        X
      </button>
    </div>

    <div class="col-12 small text-muted text-break descripcion-item">
      {{ descripcion }}
    </div>

    <div class="col-6 p-0 ps-1 pb-1">
      <img v-bind:src="imgURL" class="img-fluid w-100" v-bind:alt="codigo" />
    </div>

    <div class="col-1 p-0 text-center my-auto">
      <h6>x</h6>
      <h6>=</h6>
    </div>

    <div class="col-4 p-0 text-truncate my-auto">
      <h6>{{ cantidad }}</h6>
      <h6>{{ total.toFixed(2) }}€</h6>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  name: "ItemCarrito",
  props: {
    codigo: String,
    descripcion: String,
    cantidad: Number,
    precio: Number,
    img: String,
    categoria: String,
  },
  data() {
    return {
      deleteVisible: false,
      total: this.cantidad * this.precio,
    };
  },
  computed: {
    imgURL: function () {
      // si se ha generado con URL.createObjectURL()
      // al insertar un nuevo Item no hace falta hacer require()
      return !this.img.includes("blob")
        ? require(`../../../src/assets/${this.img}`)
        : this.img;
    },
    totalItem: function () {
      return this.cantidad * this.precio;
    },
  },
  watch: {
    // animacion fancy del total al insertar
    // un nuevo item en el carrito
    totalItem(n) {
      gsap.to(this, { duration: 0.5, total: Number(n) || 0 });
    },
  },
  methods: {
    eliminarItemCarrito: function () {
      this.$emit("eliminar-item-carrito", this.categoria, { ...this.$props });
    },
    visualizarBoton: function () {
      this.deleteVisible = true;
    },
    esconderBoton: function () {
      this.deleteVisible = false;
    },
  },
};
</script>

<style scoped>
.item-carrito {
  background-color: white;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.descripcion-item {
  overflow-y: scroll;
  min-height: 45px;
  max-height: 45px;
}
</style>