<template>
  <component :is="visibleAhora" v-bind="parametros"></component>
</template>

<script>
import routes from "../routes.js";
import EventBus from "../EventBus.js";

export default {
  name: "RouterView",
  created() {
    this.obtenerRuta();
    EventBus.$on("navegar", () => this.obtenerRuta());
  },
  data() {
    return {
      visibleAhora: null,
      parametros: null,
    };
  },
  methods: {
    obtenerRuta() {
      let indice = routes.findIndex((route) => {
        return route.path == window.location.pathname;
      });

      // Si no encuentra el indice del componente entonces muestra el componente con indice 0
      if (indice == -1) {
        indice = 0;
      }

      this.visibleAhora = routes[indice].component;
      this.parametros = routes[indice].params;
    },
  },
};
</script>