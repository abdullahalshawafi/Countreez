<template>
  <div class="row countries-list">
    <div v-for="country in countries" :key="country.name" class="col-3 gap-3">
      <router-link
        :to="{ name: 'country-details', params: { code: country.alpha3Code } }"
      >
        <article class="card">
          <div class="card-image">
            <img :src="country.flag" :alt="country.name + ' flag'" />
          </div>
          <div class="card-details">
            <h2>{{ country.name }}</h2>
            <div>
              <p>
                <span class="fw-600">Population:</span>
                {{ country.population.toLocaleString() }}
              </p>
              <p><span class="fw-600">Region:</span> {{ country.region }}</p>
              <p><span class="fw-600">Capital:</span> {{ country.capital }}</p>
            </div>
          </div>
        </article>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "countries-list-component",
  props: ["countries"],
};
</script>

<style lang="scss" scoped>
.countries-list {
  margin: 3rem calc(5rem - 30px);

  & > div {
    margin-bottom: 50px;
  }
}
</style>
