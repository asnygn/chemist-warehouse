<script>
import axios from "axios";

export default {
  data() {
    return {
      loading: false,
      error: false,
      data: null,
    };
  },
  methods: {
    async fetchData() {},
  },
  mounted() {},
};
</script>

<template>
  <!-- Main Header -->
  <MainHeader />
  <section class="sub-products"></section>
  <!-- Main Footer -->
  <MainFooter />
</template>

<style scoped>
.sub-products {
  padding: 200px 0;
}
</style>
