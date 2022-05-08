<template>
  <div class="carrito position-fixed">
    <div class="items-carrito rounded-2">
      <!-- Animaciones y tal -->
      <TransitionGroup name="items-carrito">
        <ItemCarrito
          v-for="item in items.slice().reverse()"
          v-bind:key="item.codigo"
          v-bind="item"
          v-on:eliminar-item-carrito="eliminarItemCarrito"
        />
      </TransitionGroup>
    </div>

    <div class="total-carrito rounded-2 mt-1 p-0 m-0">
      <div class="row align-items-center h-100 p-0 m-0 pb-1 pt-1 pe-1">
        <div class="col-7 h-100 d-flex align-items-center pt-2">
          <div class="w-100 h4 text-center">{{ total.toFixed(2) }}€</div>
        </div>
        <div class="col-5 p-0 h-100">
          <button
            type="button"
            class="btn btn-outline-dark border-0 w-100 h-100"
            @click="realizarPedido"
          >
            Realizar pedido
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ItemCarrito from "./ItemCarrito.vue";
import gsap from "gsap";

export default {
  name: "SeccionCarrito",
  props: {
    items: Array,
  },
  data() {
    return {
      total: 0, //para animacion fancy
    };
  },
  computed: {
    // calcula el total del carrito con
    // una propiedad de tipo computed
    totalCarrito: function () {
      return this.items.reduce(
        (itemA, itemB) => itemA + itemB.cantidad * itemB.precio,
        0
      );
    },
  },
  watch: {
    // animacion fancy del total al insertar
    // un nuevo item en el carrito
    totalCarrito(n) {
      gsap.to(this, { duration: 0.5, total: Number(n) || 0 });
    },
  },
  methods: {
    eliminarItemCarrito: function (categoria, item) {
      this.$emit("eliminar-item-carrito", categoria, item);
    },
    realizarPedido: function () {
      this.$emit("realizar-pedido");
    },
  },
  components: { ItemCarrito },
};
</script>

<style scoped>
.btn {
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.btn-outline-dark {
  background-color: white;
}

.carrito {
  height: 100%;
  width: inherit;
}

.carrito .items-carrito {
  height: 89%;
  overflow-y: scroll;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  backdrop-filter: blur(6px);
}

.carrito .total-carrito {
  height: 9%;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  backdrop-filter: blur(6px);
}

/* ejemplo de  https://vuejs.org/guide/built-ins/transition-group.html bastante nice*/
.items-carrito-move, /* apply transition to moving elements */
.items-carrito-enter-active {
  transition: all 0.5s ease;
}

.items-carrito-enter-from,
.items-carrito-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.items-carrito-leave-active {
  transition: all 0.5s ease;
  position: absolute;
}
</style>