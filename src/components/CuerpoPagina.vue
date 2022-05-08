<template>
  <div class="container-lg align-items-center">
    <div class="row g-2 vh-100">
      <div class="col-8 col-md-9">
        <div class="d-flex justify-content-center">
          <h1></h1>
        </div>

        <!-- Herramienta de transicion propietaria de Vue -->
        <Transition name="slide-fade">
          <div
            v-if="notificacionPedido"
            className="alert alert-info text-center"
            role="alert"
          >
            Pedido realizado con exito!
          </div>
        </Transition>

        <!-- Categorias -->
        <CategoriasItems
          v-bind:items="items"
          v-on:insertar-categoria="insertarCategoria"
          v-on:insertar-nuevo-item="insertarNuevoItem"
          v-on:insertar-item-carrito="insertarItemCarrito"
        />
      </div>

      <div class="col-4 col-md-3">
        <div class="d-flex justify-content-center">
          <h1></h1>
        </div>

        <!-- Carrito -->
        <SeccionCarrito
          v-bind:items="itemsCarrito"
          v-on:eliminar-item-carrito="eliminarItemCarrito"
          v-on:realizar-pedido="realizarPedido"
        />
      </div>
    </div>
  </div>
</template>

<script>
import CategoriasItems from "./categorias/CategoriasItems.vue";
import SeccionCarrito from "./carrito/SeccionCarrito.vue";

export default {
  name: "CuerpoPagina",
  data() {
    return {
      items: {
        Portatiles: [
          {
            codigo: "14ITL05",
            stock: 27,
            descripcion:
              "Lenovo IdeaPad 5 Lite 14ITL05 Intel Core i5-1135G7/8GB/512GB SSD/14.1",
            precio: 639.99,
            img: "p1.webp",
          },
          {
            codigo: "SGBOOK2",
            stock: 10,
            descripcion:
              "Samsung Galaxy Book2 Pro Intel Core i5-1240P/16GB/512GB SSD/13.3",
            precio: 1349.57,
            img: "p2.webp",
          },
          {
            codigo: "G513IC",
            stock: 47,
            descripcion:
              "Asus ROG Strix G15 G513IC-HN004 AMD Ryzen 7 4800H/16GB/512GB SSD/RTX 3050/15.6",
            precio: 949.23,
            img: "p3.webp",
          },
          {
            codigo: "16-d0057",
            stock: 10,
            descripcion:
              "HP Victus 16-d0057ns Intel Core i7-11800H/16GB/512GB SSD/RTX 3060/16.1",
            precio: 1149,
            img: "p4.webp",
          },
          {
            codigo: "G513QM",
            stock: 29,
            descripcion:
              "Asus ROG G513QM-HF070 AMD Ryzen 9 5900HX/16GB/1TB SSD/RTX3060/15.6",
            precio: 1399,
            img: "p5.webp",
          },
          {
            codigo: "RZBL15",
            stock: 5,
            descripcion:
              "Razer Blade 15 Advanced Model 4K 144Hz Intel Core i9-12900H/32GB/1TB SSD/RTX 3080Ti/15.6",
            precio: 4806.84,
            img: "p6.webp",
          },
          {
            codigo: "A10SE",
            stock: 12,
            descripcion:
              "MSI Creator 17 A10SE-627ES Intel Core i7-10875H/32GB/1TB SSD/RTX 2060/17.3",
            precio: 1828.74,
            img: "p7.webp",
          },
          {
            codigo: "V14 G2",
            stock: 45,
            descripcion:
              "Lenovo V14 G2 ITL Intel Core i5-1135G7/8GB/256GB SSD/14",
            precio: 549.99,
            img: "p8.webp",
          },
        ],
        Televisores: [
          {
            codigo: "XR50X90",
            stock: 6,
            descripcion: "Sony Bravia XR50X90JAEP 50' UltraHD 4K HDR10",
            precio: 799.99,
            img: "t1.webp",
          },
          {
            codigo: "XR55A80",
            stock: 11,
            descripcion: "Sony Bravia XR55A80JAEP 55' OLED UltraHD 4K HDR",
            precio: 1874.07,
            img: "t2.webp",
          },
          {
            codigo: "QE65Q95",
            stock: 1,
            descripcion: "Samsung QE65Q950TS 65' QLED UltraHD 8K HDR10+",
            precio: 5073.99,
            img: "t3.webp",
          },
          {
            codigo: "QE85QN85",
            stock: 12,
            descripcion: "Sasmung QE85QN85AAT 85' Neo QLED UltraHD 4K",
            precio: 639.99,
            img: "t4.webp",
          },
        ],
        Perifericos: [
          {
            codigo: "Apple Airpods G",
            stock: 12,
            descripcion: "Apple Airpods Max Auriculares Bluetooth Grises",
            precio: 588.75,
            img: "pf1.webp",
          },
          {
            codigo: "Apple Airpods P",
            stock: 16,
            descripcion: "Apple AirPods Max Plata",
            precio: 572.33,
            img: "pf2.webp",
          },
          {
            codigo: "Shure Aonic 4",
            stock: 9,
            descripcion: "Shure Aonic 4 Auriculares con Micrófono Blancos",
            precio: 420.99,
            img: "pf3.webp",
          },
          {
            codigo: "Logitech G Pro X",
            stock: 34,
            descripcion:
              "Logitech G Pro X Auriculares Gaming Inalámbricos con Lightspeed Negros",
            precio: 234.04,
            img: "pf4.webp",
          },
          {
            codigo: "Logitech G733",
            stock: 56,
            descripcion: "Logitech G733 Auriculares Gaming Inalámbricos Negros",
            precio: 136.78,
            img: "pf5.webp",
          },
          {
            codigo: "Logitech G305",
            stock: 163,
            descripcion:
              "Logitech G305 LightSpeed Ratón Inalámbrico Gaming 12000DPI Negro",
            precio: 29.99,
            img: "pf6.webp",
          },
          {
            codigo: "Logitech MX Master",
            stock: 234,
            descripcion:
              "Logitech MX Master 3 Ratón Inalámbrico Avanzado 4000DPI Gris",
            precio: 101.81,
            img: "pf7.webp",
          },
        ],
      },
      itemsCarrito: [],
      notificacionPedido: false,
    };
  },
  components: {
    CategoriasItems,
    SeccionCarrito,
  },
  computed: {
    // puedo calcular automaticamente las categorias
    // sin tener que repetir Object.keys() cada vez, Vue es maravilloso
    nombreCategorias: function () {
      return Object.keys(this.items);
    },

    // puedo tener todos los items en una sola lista para comprobar
    // mas facilmente duplicados de codigos de item al insertar un nuevo objeto
    listaItems: function () {
      let auxList = [];

      this.nombreCategorias.forEach((categoria) => {
        this.items[categoria].forEach((item) => auxList.push(item));
      });

      return auxList;
    },
  },
  methods: {
    insertarCategoria: function (nombre) {
      if (this.nombreCategorias.includes(nombre)) {
        alert("Ya existe una categoria con ese nombre");
      } else {
        this.items[nombre] = [];
      }
    },
    insertarNuevoItem: function (categoria, nuevoItem) {
      let itemCategoria = this.listaItems.find(function (item) {
        return item.codigo === nuevoItem.codigo;
      });

      if (itemCategoria === undefined) {
        this.items[categoria].push(nuevoItem);
      } else {
        alert("Un item con ese codigo ya existe");
      }
    },
    insertarItemCarrito: function (categoria, nuevoItem) {
      // busca el item en el carrito
      let itemCarrito = this.itemsCarrito.find(function (item) {
        return item.codigo === nuevoItem.codigo;
      });

      // si el item no se encuentra en el carrito añadelo
      if (itemCarrito === undefined) {
        nuevoItem.cantidad = 1;
        nuevoItem.categoria = categoria;

        this.itemsCarrito.push(nuevoItem);
      } else {
        // aumenta la cantidad del item en el acrrito
        this.itemsCarrito = this.itemsCarrito.map((item) => {
          if (item.codigo === nuevoItem.codigo) {
            item.cantidad += 1;
          }
          return JSON.parse(JSON.stringify(item));
        });
      }

      // en cualquiera de los casos anteriores
      // el stock del item se reduce en 1
      this.items[categoria] = this.items[categoria].map((item) => {
        if (item.codigo === nuevoItem.codigo) {
          item.stock -= 1;
        }
        return JSON.parse(JSON.stringify(item));
      });
    },
    eliminarItemCarrito: function (categoria, itemEliminar) {
      // si el item no se encuentra en el carrito añadelo
      if (itemEliminar.cantidad - 1 <= 0) {
        this.itemsCarrito = this.itemsCarrito.filter((item) => {
          return item.codigo != itemEliminar.codigo;
        });
      } else {
        // disminuye en 1 la cantidad del item en el carrito
        this.itemsCarrito = this.itemsCarrito.map((item) => {
          if (item.codigo === itemEliminar.codigo) {
            item.cantidad -= 1;
          }
          return JSON.parse(JSON.stringify(item));
        });
      }

      // en cualquiera de los casos anteriores
      // el stock del item se reduce en 1
      this.items[categoria] = this.items[categoria].map((item) => {
        if (item.codigo === itemEliminar.codigo) {
          item.stock += 1;
        }
        return JSON.parse(JSON.stringify(item));
      });
    },
    realizarPedido: function () {
      if (this.notificacionPedido) {
        this.notificacionPedido = false;
      } else {
        if (this.itemsCarrito.length === 0) {
          alert("Su carrito esta vacio!");
        } else {
          (this.notificacionPedido = true), (this.itemsCarrito = []);
        }
      }
    },
  },
};
</script>

<style scoped>
.slide-fade-enter-active {
  transition: all 0.5s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.5s ease-out;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

.alert {
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}
</style>
