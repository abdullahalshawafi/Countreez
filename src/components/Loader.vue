<template>
  <loading
    v-model:active="isLoading"
    :is-full-page="false"
    loader="bars"
    color="#111517"
  />
</template>

<script>
import { ref, watchEffect } from "vue";
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";

export default {
  name: "loader-component",
  props: ["loading"],
  components: { Loading },
  setup(props) {
    const isLoading = ref(true);

    watchEffect(() => {
      isLoading.value = props.loading;
    });

    return { isLoading };
  },
};
</script>

<style></style>
