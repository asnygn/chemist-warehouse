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
          "https://cw-api.zino.tech/homepage/list"
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
  <MainHeader />
  <Container v-show="loading">
    <Loading :pageLoading="true" />
  </Container>
  <WelcomeImage
    :title="data?.list?.[0].block1SmallText"
    :description="data?.list?.[0].block1LargeText"
    imageUrl="/image/warehouse.jpg"
    v-if="data"
  />
  <!-- Our Commitment -->
  <div class="section2" v-if="data">
    <Container>
      <div class="section2__text-wrapper">
        <div class="section2__text1">
          <p>{{ data?.list?.[0].block2Title }}</p>
        </div>
        <div class="section2__text2">
          <p>{{ data?.list?.[0].block2Text }}</p>
        </div>
      </div>
    </Container>
  </div>
  <!-- Our Services -->
  <div class="section3" v-if="data && data?.list?.[0].services">
    <Container>
      <div class="section3__title">
        <h3>Our Services</h3>
      </div>
      <div class="section3__block-wrapper">
        <div class="section3__block" v-for="item in data?.list?.[0].services">
          <div class="section3__block-content">
            <div
              class="section3__block-image"
              v-bind:style="{
                'background-image': 'url(' + item.image + ')',
              }"
            ></div>
            <div>
              <div class="section3__block-title">
                <h3>{{ item.title }}</h3>
              </div>
              <div class="section3__block-description">
                <p>{{ item.description }}</p>
              </div>
            </div>
            <div class="section3__block-link">
              <RouterLink to="/products">Read more...</RouterLink>
            </div>
          </div>
        </div>
      </div>
    </Container>
  </div>
  <!-- Our Products -->
  <div class="section4" v-if="data && data?.list?.[0].products">
    <Container>
      <div class="section4__title">
        <h3>Our Products</h3>
      </div>
      <div class="section4__block-wrapper">
        <masonry-wall
          :items="data?.list?.[0].products"
          :ssr-columns="1"
          :column-width="400"
          :gap="16"
          :min-columns="1"
          :max-columns="2"
        >
          <template #default="{ item, index }">
            <div class="section4__block">
              <div class="section4__image">
                <ImageLoader
                  :imageUrl="item.image"
                  loadingStyle="height:200px;"
                />
              </div>
              <div class="section4__text-wrapper">
                <div class="section4__block-title">
                  <h3>{{ item.title }}</h3>
                </div>
                <div class="section4__block-description">
                  <p>
                    {{ item.description }}
                  </p>
                </div>
              </div>
            </div>
          </template>
        </masonry-wall>
      </div>
      <div class="section4__footer">
        <div class="section4__more">
          <RouterLink class="button-primary" to="/products">
            More Products
          </RouterLink>
        </div>
      </div>
    </Container>
  </div>
  <!-- Our Customers -->
  <div class="section5" v-if="data && data?.list?.[0].customers">
    <Container>
      <div class="section5__text1">
        <h2>Our Customers</h2>
      </div>
      <div class="section5__text2">
        <p>Proud To Work With</p>
      </div>
      <div class="section5__content">
        <div v-for="item in data?.list?.[0].customers">
          <img :src="item.image" />
        </div>
      </div>
    </Container>
  </div>
  <MainFooter v-if="data" />
</template>

<style scoped>
.section2 {
  position: relative;
  padding: 100px 0;
  background-color: #1e3a80;
}
.section2__text-wrapper {
  display: flex;
  flex: 1;
  align-items: center;
}
.section2__text1 {
  flex-basis: 30%;
  margin-right: 80px;
  margin-bottom: 20px;
  font-size: 30px;
  font-weight: bold;
  color: #fff;
}
.section2__text2 {
  flex-basis: 70%;
  font-size: 18px;
  font-weight: 400;
  line-height: 1.5;
  color: #fff;
}

.section3 {
  position: relative;
  padding: 100px 0;
  background-color: #fff;
}

.section3__title {
  margin-bottom: 80px;
  text-align: center;
  font-size: 30px;
  font-weight: 400;
  color: #2e2e2e;
}
.section3__title h3 {
  display: inline;
  position: relative;
}
.section3__title h3::before {
  position: absolute;
  bottom: -10px;
  content: "";
  width: 90%;
  height: 4px;
  background-color: #1e3a80;
}

.section3__block {
  position: relative;
  padding: 40px 20px;
  background-color: #0e2460;
}

.section3__block-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.section3__block-image {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
}
.section3__block-image::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(14, 36, 96, 0.5);
}

.section3__block-title,
.section3__block-description,
.section3__block-link {
  position: relative;
  z-index: 1;
}

.section3__block-title {
  margin-bottom: 20px;
}
.section3__block-title h3 {
  font-size: 20px;
  font-weight: 500;
  color: #fff;
}

.section3__block-description {
  margin-bottom: 20px;
  font-size: 16px;
  font-weight: 400;
  color: #fff;
}

.section3__block-link a {
  font-size: 14px;
  font-weight: 400;
  color: #fff;
  text-decoration: underline;
}
.section3__block-link a:hover {
  text-decoration: underline;
}

.section3__title h3 {
  display: inline;
  position: relative;
}
.section3__title h3::before {
  position: absolute;
  bottom: -10px;
  content: "";
  width: 90%;
  height: 4px;
  background-color: #1e3a80;
}

.section3__block-wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 2rem;
}

.section4 {
  position: relative;
  padding: 100px 0;
  background-color: #f4f5f6;
}

.section4__title {
  margin-bottom: 80px;
  text-align: center;
  font-size: 30px;
  font-weight: 400;
  color: #2e2e2e;
}
.section4__title h3 {
  display: inline;
  position: relative;
}
.section4__title h3::before {
  position: absolute;
  bottom: -10px;
  content: "";
  width: 90%;
  height: 4px;
  background-color: #1e3a80;
}

.section4__block-wrapper {
  max-width: 820px;
  margin: 0 auto;
}

.section4__block {
  background-color: #fff;
}

.section4__text-wrapper {
  padding: 20px;
}

.section4__block-title h3 {
  margin-bottom: 20px;
  font-size: 20px;
  font-weight: 400;
  color: #2e2e2e;
}

.section4__block-description {
  font-size: 14px;
  font-weight: 400;
  color: #858585;
}

.section4__footer {
  margin-top: 80px;
}

.section4__more {
  text-align: center;
}
.button-primary {
  display: inline-block;
  padding: 15px 40px;
  text-decoration: none;
  font-size: 12px;
  color: #fff;
  background-color: #0e2460;
  border-radius: 40px;
}

.section5 {
  position: relative;
  padding: 100px 0;
  background-color: #fff;
}

.section5__text1 {
  margin-bottom: 20px;
}
.section5__text1 h2 {
  font-size: 20px;
  font-weight: 400;
  text-align: center;
  color: #989898;
}

.section5__text2 {
  margin-bottom: 40px;
  font-size: 40px;
  font-weight: bold;
  text-align: center;
  color: #595959;
}

.section5__content {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  margin-top: 80px;
  max-width: 600px;
  margin: 0 auto;
}
.section5__content > div {
  flex-grow: 1;
  width: 33%;
  text-align: center;
}

@media screen and (max-width: 860px) {
  .section2 {
    padding: 50px 0;
  }
  .section2__text-wrapper {
    display: block;
  }

  .section3__block-wrapper {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 680px) {
  .section3__block-wrapper {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
