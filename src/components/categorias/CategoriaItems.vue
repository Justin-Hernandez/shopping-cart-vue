<template>
  <div
    class="btn w-100 mb-1 border-0"
    @click="visualizar"
    v-bind:class="visible ? 'btn-dark' : 'btn-outline-dark'"
  >
    {{ categoria }}
  </div>

  <div
    class="rounded-2 div-categoria"
    v-bind:class="
      visible === null
        ? 'categoria-inicial'
        : visible
        ? 'categoria-visible'
        : 'categoria-escondida'
    "
  >
    <div class="row m-0 p-0">
      <div
        class="col-3 m-0 p-0 pt-0 pb-1 pe-1"
        v-for="(item, index) in items"
        v-bind:key="index"
      >
        <ItemCard
          v-bind="item"
          v-bind:categoria="categoria"
          v-bind:columna="index + 1"
          v-on:insertar-item-carrito="insertarItemCarrito"
        />
      </div>

      <NuevoItemCard
        v-bind:categoria="categoria"
        v-on:insertar-nuevo-item="insertarNuevoItem"
      />
    </div>
  </div>
</template>

<script>
import ItemCard from "../items/ItemCard.vue";
import NuevoItemCard from "../items/NuevoItemCard.vue";

export default {
  name: "CategoriaItems",
  props: {
    categoria: String,
    items: Array,
  },
  data() {
    return {
      visible: null,
    };
  },
  components: {
    ItemCard,
    NuevoItemCard,
  },
  emits: ["insertar-nuevo-item", "insertar-item-carrito"],
  methods: {
    visualizar: function () {
      if (this.visible === null) {
        this.visible = true;
      } else {
        this.visible = !this.visible;
      }
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
.div-categoria {
  overflow-y: scroll;
  backdrop-filter: blur(7px);
}

.btn {
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.btn-outline-dark {
  background-color: white;
}

.categoria-inicial {
  height: 0;
  opacity: 0;
}

.categoria-escondida {
  animation: slide-inverso 0.5s forwards;
}

.categoria-visible {
  animation: slide 0.5s forwards;
}

@keyframes slide {
  from {
    height: 0;
    opacity: 0;
  }
  to {
    height: 450px;
    opacity: 1;
  }
}

@keyframes slide-inverso {
  from {
    height: 450px;
    opacity: 1;
  }
  to {
    height: 0;
    opacity: 0;
  }
}
</style>
