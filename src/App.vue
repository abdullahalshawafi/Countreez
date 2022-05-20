<template>
  <Navbar :mode="colorsMode" @toggle-mode="toggleMode" />
  <router-view />
</template>

<script>
import AOS from "aos";
import axios from "axios";
import { onMounted, ref } from "vue";
import Navbar from "@/components/Navbar.vue";

axios.defaults.baseURL = "https://restcountries.com/v2/";

export default {
  name: "App",
  components: { Navbar },
  setup() {
    const colorsMode = ref(localStorage.getItem("mode") || "light");

    onMounted(() => {
      AOS.init();

      if (
        window.matchMedia &&
        window.matchMedia("(prefers-color-scheme: dark)").matches
      ) {
        colorsMode.value = "dark";
      } else {
        colorsMode.value = "light";
      }

      if (colorsMode.value === "dark") {
        localStorage.setItem("mode", "dark");
        document.documentElement.setAttribute("mode", "dark");
      } else {
        localStorage.setItem("mode", "light");
        document.documentElement.setAttribute("mode", "light");
      }
    });

    const toggleMode = () => {
      if (colorsMode.value === "light") {
        colorsMode.value = "dark";
        localStorage.setItem("mode", "dark");
        document.documentElement.setAttribute("mode", "dark");
      } else {
        colorsMode.value = "light";
        localStorage.setItem("mode", "light");
        document.documentElement.setAttribute("mode", "light");
      }
    };

    return {
      colorsMode,
      toggleMode,
    };
  },
};
</script>

<style lang="scss">
@import "./assets/scss/globals";
</style>
