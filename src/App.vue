<template>
  <CuerpoPagina />
</template>

<script>
import CuerpoPagina from "./components/CuerpoPagina.vue";

export default {
  name: "App",
  components: {
    CuerpoPagina,
  },
};
</script>

<style>
body {
  background-color: #e5e5f7;
  background-image: radial-gradient(#000000 1.6px, transparent 1.6px),
    radial-gradient(#000000 1.6px, #e5e5f7 1.6px);
  background-size: 64px 64px;
  background-position: 0 0, 32px 32px;
}

/* custom scrollbar */
::-webkit-scrollbar {
  width: 7px;
}

::-webkit-scrollbar-track {
  background-color: transparent;
}

::-webkit-scrollbar-thumb {
  background-color: #d6dee1;
  border-radius: 20px;
  border: 0px solid transparent;
  background-clip: content-box;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #a8bbbf;
}
</style>
