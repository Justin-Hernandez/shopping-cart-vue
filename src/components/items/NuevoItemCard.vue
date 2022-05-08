<template>
  <div class="col-3 m-0 p-0 pt-0 pb-1 pe-1">
    <Transition name="fade">
      <div v-if="mostrarForm" class="card border-0 p-0">
        <form @submit.prevent="insertarNuevoItem">
          <div class="card-body p-2 pb-0">
            <div class="col-12 form-floating pb-3">
              <input
                v-model="codigo"
                required
                name="codigo"
                class="form-control input-sm border-0"
                type="text"
                maxLength="10"
                id="codigo"
                placeholder="XXXX"
              />
              <label htmlFor="codigo" class="text-break">Codigo</label>
            </div>

            <div class="col-12 form-floating pb-3">
              <input
                v-model="stock"
                required
                name="stock"
                class="form-control input-sm border-0"
                type="number"
                min="1"
                max="999"
                step="1"
                id="stock"
                placeholder="99"
              />
              <label htmlFor="stock" class="text-break">Stock</label>
            </div>

            <div class="col-12 form-floating pb-3">
              <input
                v-model="precio"
                required
                name="precio"
                class="form-control input-sm border-0"
                type="number"
                min="0.1"
                max="9999.99"
                step="0.01"
                id="precio"
                placeholder="99.99"
              />
              <label htmlFor="precio" class="text-break">Precio</label>
            </div>

            <div class="col-12 form-floating pb-3">
              <textarea
                v-model="descripcion"
                required
                name="descripcion"
                id="descripcion"
                class="form-control input-sm border-0"
                placeholder="Descripcion..."
              ></textarea>
              <label htmlFor="descripcion" class="text-break"
                >Descripcion</label
              >
            </div>

            <div class="col-12 pb-1">
              <input
                v-on:change="imageFileOnChange"
                required
                name="img"
                class="form-control"
                type="file"
                id="form-img"
                accept="image/*"
              />
            </div>
          </div>

          <div class="card-footer border-0 p-2">
            <button
              type="submit"
              class="btn btn-outline-dark w-100 border-0 mb-1"
            >
              Crear
            </button>
            <button
              type="button"
              class="btn btn-outline-danger w-100 border-0"
              @click="toggleForm"
            >
              Cancelar
            </button>
          </div>
        </form>
      </div>
      <div v-else class="card border-0" @click="toggleForm">
        <div class="card-header border-0 mt-1 mb-5">{{ " " }}</div>

        <img
          src="../../../src/assets/add.png"
          class="card-img-top mt-4 mb-5"
          alt=""
        />

        <div class="card-footer border-0 mt-5">{{ " " }}</div>
      </div>
    </Transition>
  </div>
</template>

<script>
export default {
  name: "ItemCard",
  props: {
    categoria: String,
  },
  data() {
    return {
      mostrarForm: false,
      codigo: "",
      descripcion: "",
      stock: "",
      precio: "",
      img: "",
    };
  },
  computed: {},
  methods: {
    insertarNuevoItem: function () {
      let nuevoItem = {
        codigo: this.codigo,
        descripcion: this.descripcion,
        stock: this.stock,
        precio: this.precio,
        img: this.img,
      };

      // emite evento capturado por el padre para insertar el nuevo item]
      this.$emit("insertar-nuevo-item", this.categoria, nuevoItem);

      // resetea los valores del form
      this.codigo = "";
      this.descripcion = "";
      this.stock = "";
      this.precio = "";
      this.img = "";

      this.toggleForm();
    },
    imageFileOnChange: function (event) {
      this.img = URL.createObjectURL(event.target.files[0]);
    },
    toggleForm: function () {
      this.mostrarForm = !this.mostrarForm;
    },
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

input,
textarea {
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.btn-outline-dark,
.btn-outline-danger {
  background-color: white;
}

.fade-enter-active {
  transition: all 0.2s;
}

.fade-leave-active {
  transition: all 0s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>