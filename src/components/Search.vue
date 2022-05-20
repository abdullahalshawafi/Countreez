<template>
  <form @submit.prevent="">
    <label for="country">
      <i class="fa fa-search"></i>
      <input
        type="text"
        name="country"
        placeholder="Search for a country..."
        id="country"
        autocomplete="off"
        v-model.trim="search"
      />
    </label>
  </form>
</template>

<script>
import { ref, watch } from "vue";

export default {
  name: "search-component",
  setup(_, { emit }) {
    const search = ref("");
    const debounce = ref(null);

    watch(
      () => search.value,
      () => {
        if (debounce.value) {
          clearTimeout(debounce.value);
        }
        debounce.value = setTimeout(() => {
          emit("search", search.value.toLowerCase());
        }, 200);
      }
    );

    return { search };
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/mixins";

form {
  @include element-style;

  margin-top: 2rem;
  padding: 1rem 1.5rem;

  label {
    display: flex;

    i {
      color: var(--text-color);
    }

    input {
      width: 100%;
      border: none;
      background-color: transparent;
      color: var(--text-color);
      margin-left: 1.5rem;

      &:focus {
        outline: none;
      }

      &::placeholder {
        color: var(--input-color);
      }
    }
  }
}
</style>
