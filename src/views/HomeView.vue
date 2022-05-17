<template>
  <main>
    <div class="search-filter-wrapper">
      <Search />
    </div>
  </main>
</template>

<script>
import Search from "@/components/Search.vue";
export default {
  name: "HomeView",
  components: { Search },
};
</script>

<style lang="scss" scoped>
main {
  font-size: 14px;
}
.search-filter-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2rem 5rem 0 5rem;
}
</style>
