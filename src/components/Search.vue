<template>
  <form>
    <label for="country">
      <i class="fa fa-search"></i>
      <input
        type="text"
        name="country"
        placeholder="Search for a country..."
        id="country"
        autocomplete="off"
      />
    </label>
  </form>
</template>

<script>
export default {
  name: "search-component",
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables";

form {
  background-color: var(--elements-color);
  box-shadow: 0 0px 10px -3px rgb(0 0 0 / 20%);
  padding: 1rem 1.5rem;
  border-radius: 5px;
  width: 35%;

  label {
    display: flex;

    i {
      color: var(--text-color);
    }

    input {
      width: 100%;
      border: none;
      background-color: transparent;
      color: var(--input-color);
      margin-left: 1.5rem;

      &:focus {
        outline: none;
      }
    }
  }
}
</style>
