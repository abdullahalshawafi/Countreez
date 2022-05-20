<template>
  <div ref="dropdownList" class="dropdown" @click="toggleDropdown">
    <span>
      {{ filter || "Filter by Region" }}
      <i v-if="filter" class="fas fa-xmark" @click="$emit('clear-filter')"></i>
      <i
        v-else
        :class="isDropdownShown ? 'fa fa-angle-up' : 'fa fa-angle-down'"
      ></i>
    </span>
    <ul class="dropdown-list">
      <li
        v-for="region in regions"
        :key="region"
        class="dropdown-item"
        @click="$emit('filter', region)"
      >
        {{ region }}
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, watchEffect } from "vue";

export default {
  name: "filter-component",
  props: ["filter"],
  setup() {
    const dropdownList = ref(null);
    const isDropdownShown = ref(false);
    const regions = ref(["Africa", "Americas", "Asia", "Europe", "Oceania"]);

    const closeDropdown = (e) => {
      if (!dropdownList.value.contains(e.target)) {
        isDropdownShown.value = false;
        dropdownList.value.classList.remove("show");
        window.removeEventListener("click", closeDropdown);
      }
    };

    watchEffect(() => {
      if (isDropdownShown.value) {
        window.addEventListener("click", closeDropdown);
      }
    });

    const toggleDropdown = () => {
      dropdownList.value.classList.toggle("show");
      isDropdownShown.value = !isDropdownShown.value;
    };

    return {
      dropdownList,
      isDropdownShown,
      regions,
      toggleDropdown,
    };
  },
};
</script>

<style lang="scss" scoped>
.dropdown {
  margin-top: 2rem;

  span {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
  }
}
</style>
