<template>
  <main>
    <div
      class="row justify-content-between align-items-start search-filter-wrapper"
    >
      <Search class="col-5" @search="searchCountries" />
      <Filter
        class="col-2"
        @clear-filter="clearFilter"
        @filter="setFilter"
        :filter="filter"
      />
    </div>
    <div>
      <loading
        v-model:active="isLoading"
        :is-full-page="false"
        loader="bars"
        color="#111517"
      />
      <CountriesList :countries="countries" />
    </div>
  </main>
</template>

<script>
import { onMounted, ref, watchEffect } from "vue";
import axios from "axios";
import Loading from "vue-loading-overlay";
import Search from "@/components/Search.vue";
import Filter from "@/components/Filter.vue";
import CountriesList from "@/components/CountriesList.vue";

import "vue-loading-overlay/dist/vue-loading.css";

export default {
  name: "HomeView",
  components: { Search, Filter, Loading, CountriesList },
  setup() {
    const isLoading = ref(false);
    const allCountries = ref(
      JSON.parse(sessionStorage.getItem("countries")) || []
    );
    const countries = ref(
      JSON.parse(sessionStorage.getItem("countries")) || []
    );
    const filter = ref("");

    onMounted(async () => {
      if (!allCountries.value.length) {
        isLoading.value = true;
        try {
          const response = await axios.get("all");
          allCountries.value = response.data;
          countries.value = response.data;
          sessionStorage.setItem("countries", JSON.stringify(response.data));
        } catch (error) {
          alert("Couldn't fetch countries data!");
        } finally {
          isLoading.value = false;
        }
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
  padding: 2rem 5rem 0 5rem;
}
</style>
