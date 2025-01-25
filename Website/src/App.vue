<template>
  <div :class="themeClass" id="app">
    <Navbar :isDarkMode="isDarkMode" />

    <div>
      
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";

export default {
  components: {
    Navbar,
  },
  data() {
    return {
      isDarkMode: false, 
    };
  },
  computed: {
    themeClass() {
      return this.isDarkMode ? "dark" : "light"; 
    },
  },
  created() {
    // Detetar o modo escuro ou claro no navegador
    this.isDarkMode = window.matchMedia("(prefers-color-scheme: dark)").matches;

    // Adicionar listener para mudanças no modo de cor do sistema
    window.matchMedia("(prefers-color-scheme: dark)").addEventListener("change", (e) => {
      this.isDarkMode = e.matches;
    });
  },
};
</script>

<style>

body{
  margin: 0;
  font-family: Arial, sans-serif;
  min-height: 100vh;
  width: 100%;
  display: flex;
  overflow-x: hidden;
}

#app {
  margin: 0;
  font-family: Arial, sans-serif;
  min-height: 100vh;
  width: 100%;
  display: flex;
  overflow-x: hidden;
}

/* Tema claro */
.light {
  background-color: #f0f0f0;
  color: #333;
}

/* Tema escuro */
.dark {
  background-color: #333;
  color: #f0f0f0;
}
</style>
