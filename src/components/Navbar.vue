<template>
  <header>
    <nav class="navbar">
      <router-link to="/" class="navbar-legend">
        <h1>Where in the world?</h1>
      </router-link>
      <span
        v-if="mode === 'light'"
        @click="$emit('toggle-mode')"
        class="cursor-pointer clickable fw-600"
      >
        <i class="fa-regular fa-moon"></i> Dark Mode
      </span>
      <span
        v-else
        @click="$emit('toggle-mode')"
        class="cursor-pointer clickable fw-600"
      >
        <i class="fa-regular fa-sun"></i> Light Mode
      </span>
    </nav>
  </header>
</template>

<script>
export default {
  name: "navbar-component",
  props: ["mode"],
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables";

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 5rem;
  background-color: var(--elements-color);
  box-shadow: 0 9px 10px -13px rgb(0 0 0 / 20%);

  a.navbar-legend {
    color: var(--text-color);
    text-decoration: none;
  }
}
</style>
