<template>
  <main>
    <div
      class="row justify-content-between align-items-start search-filter-wrapper"
    >
      <Search class="col-5 col-md-7 col-sm-12" @search="searchCountries" />
      <Filter
        class="col-2 col-md-4 col-sm-8"
        @clear-filter="clearFilter"
        @filter="setFilter"
        :filter="filter"
      />
    </div>
    <div>
      <Loader :loading="isLoading" />
      <CountriesList :countries="countries" />
    </div>
  </main>
</template>

<script>
import { onMounted, ref, watchEffect } from "vue";
import axios from "axios";

import Search from "@/components/Search.vue";
import Filter from "@/components/Filter.vue";
import Loader from "@/components/Loader.vue";
import CountriesList from "@/components/CountriesList.vue";

export default {
  name: "HomeView",
  components: { Search, Filter, Loader, CountriesList },
  setup() {
    const isLoading = ref(false);
    const allCountries = ref([]);
    const countries = ref([]);
    const filter = ref("");

    onMounted(async () => {
      isLoading.value = true;
      try {
        const response = await axios.get(
          "all?fields=name,flag,population,region,capital"
        );
        allCountries.value = response.data;
        countries.value = response.data;
      } catch (error) {
        alert("Couldn't fetch countries data!");
      } finally {
        isLoading.value = false;
      }
    });

    watchEffect(() => {
      if (filter.value === "") {
        return;
      }

      countries.value = allCountries.value.filter(
        (country) => country.region === filter.value
      );
    });

    const searchCountries = (search) => {
      countries.value = allCountries.value.filter((country) => {
        return country.name.toLowerCase().includes(search);
      });
    };

    const clearFilter = () => {
      countries.value = allCountries.value;
      filter.value = "";
    };

    const setFilter = (region) => {
      filter.value = region;
    };

    return {
      isLoading,
      countries,
      filter,
      searchCountries,
      clearFilter,
      setFilter,
    };
  },
};
</script>

<style lang="scss" scoped>
main {
  font-size: 14px;
}

.search-filter-wrapper {
  padding: 0 var(--x-gutter);
}
</style>
