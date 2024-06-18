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
    async fetchData() {
      this.loading = true;
      try {
        const response = await axios.post(
          "https://cw-api.zino.tech/products/list"
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
    this.fetchData();
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
    title="Products / Services"
    :description="data?.list?.[0].h1Text"
    imageUrl="/image/products.jpg"
    v-if="data"
  />
  <!-- Products -->
  <section class="products" v-if="data && data?.list?.[0].products">
    <Container>
      <div class="product" v-for="(product, index) in data?.list?.[0].products">
        <div class="product__layout">
          <div class="product__number">
            {{ String(++index).padStart(2, 0) }}.
          </div>
          <div class="product__title">{{ product.title }}</div>
          <div class="product__description">
            {{ product.description }}
          </div>
        </div>
        <div class="product__layout">
          <div class="product__image">
            <img :src="product.image" />
          </div>
        </div>
      </div>
    </Container>
  </section>
  <!-- Main Footer -->
  <MainFooter v-if="data" />
</template>

<style scoped>
.products {
  padding: 100px 0;
}

.product {
  display: flex;
  margin-bottom: 100px;
}
.product .product__layout:first-child {
  margin-right: 80px;
}
.product__number {
  margin-bottom: 60px;
  font-size: 50px;
  font-weight: 500;
}
.product__title {
  margin-bottom: 20px;
  font-size: 25px;
}
.product__description {
  font-size: 18px;
  color: #7a7a7a;
  line-height: 1.5;
}

@media screen and (max-width: 860px) {
  .product {
    display: block;
  }
  .product__number {
    margin-bottom: 20px;
  }
  .product__description {
    margin-bottom: 20px;
  }
}
</style>
