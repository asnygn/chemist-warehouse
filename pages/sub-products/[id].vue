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
    async fetchData(id) {
      this.loading = true;
      try {
        const response = await axios.post(
          "https://api.chemistwarehouse.org/sub-products/list",
          { alias: id }
        );
        this.data = response.data;
      } catch (err) {
        this.error = true;
      } finally {
        this.loading = false;
      }
    },
  },
  mounted() {
    const route = useRoute();
    this.fetchData(route.params.id);
  },
};
</script>

<template>
  <!-- Main Header -->
  <MainHeader />
  <Container v-if="loading">
    <Loading :pageLoading="true" />
  </Container>
  <!-- Welcome Image -->
  <WelcomeImage
    title="Sub-Products"
    description=""
    :imageUrl="data?.list?.[0]?.body[0]?.image"
    v-if="data"
  />
  <!-- Products -->
  <section class="sub-products" v-if="data">
    <Container>
      <div class="sub-products__title">{{ data?.list?.[0]?.title }}</div>
      <div class="sub-products__body" v-for="item in data?.list?.[0]?.body">
        <div class="sub-products__text" v-if="item?.text">
          {{ item?.text }}
        </div>
        <div class="sub-products__image" v-if="item?.image">
          <img :src="item.image" />
        </div>
      </div>
    </Container>
  </section>
  <!-- Main Footer -->
  <MainFooter v-if="data" />
</template>

<style scoped>
.sub-products {
  padding: 100px 0;
}
.sub-products__title {
  margin-bottom: 20px;
  font-size: 30px;
  font-weight: 900;
  text-align: center;
}
.sub-products__text {
  margin-bottom: 40px;
  font-size: 18px;
  font-weight: 400;
  text-align: center;
  color: #7a7a7a;
}
.sub-products__image {
  margin-bottom: 40px;
}
.sub-products__image img {
  width: 100%;
  border-radius: 10px;
}
</style>
