<template>
  <Navbar :mode="colorsMode" @toggle-mode="toggleMode" />
  <router-view />
</template>

<script>
import { onMounted, ref } from "vue";
import Navbar from "@/components/Navbar.vue";

export default {
  name: "App",
  components: { Navbar },
  setup() {
    const colorsMode = ref("light");

    onMounted(() => {
      if (colorsMode.value === "dark") {
        document.documentElement.setAttribute("mode", "dark");
      } else {
        document.documentElement.setAttribute("mode", "light");
      }
    });

    const toggleMode = () => {
      if (colorsMode.value === "light") {
        colorsMode.value = "dark";
        document.documentElement.setAttribute("mode", "dark");
      } else {
        colorsMode.value = "light";
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
