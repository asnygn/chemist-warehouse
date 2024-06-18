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
          "https://cw-api.zino.tech/about/list"
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
  <!-- Loading -->
  <Container v-if="loading">
    <Loading :pageLoading="true" />
  </Container>
  <!-- Welcome Image -->
  <WelcomeImage
    title="About us"
    :description="data?.list?.[0].h1Text"
    imageUrl="/image/about.jpg"
    v-if="data"
  />
  <!-- Our Story -->
  <section class="our-story" v-if="data">
    <Container>
      <div class="our-story__body">
        <div class="our-story__text1">
          <p>Our Story</p>
        </div>
        <div class="our-story__text2">
          {{ data?.list?.[0].ourStoryBlack }}
        </div>
      </div>
    </Container>
  </section>
  <!-- Meet Our Team -->
  <section class="our-team" v-if="data && data?.list?.[0].team">
    <Container>
      <div class="our-team__title">
        <p>Meet our team</p>
      </div>
      <div class="our-team__content">
        <div class="team-member" v-for="item in data?.list?.[0].team">
          <div class="team-member__image">
            <ImageLoader
              :imageUrl="item.image"
              loadingStyle="height:200px;border-radius: 10px"
            />
          </div>
          <div class="team-member__name">{{ item.name }}</div>
          <div class="team-member__role">{{ item.position }}</div>
          <div class="team-member__description">
            {{ item.about }}
          </div>
        </div>
      </div>
    </Container>
  </section>
  <!-- Main Footer -->
  <MainFooter v-if="data" />
</template>

<style scoped>
/* Our Story */
.our-story {
  position: relative;
  padding: 100px 0;
  background-color: #fff;
}
.our-story__body {
  display: flex;
  flex: 1;
}
.our-story__text1 {
  flex-basis: 30%;
  margin-right: 80px;
  margin-bottom: 20px;
  font-size: 50px;
  font-weight: 500;
  color: #0e2460;
}
.our-story__text2 {
  flex-basis: 70%;
  font-size: 18px;
  font-weight: 400;
  line-height: 1.5;
  color: #272727;
}

/* Our Team */
.our-team {
  position: relative;
  margin-bottom: 100px;
  background-color: #fff;
}
.our-team__title {
  margin-bottom: 60px;
  font-size: 50px;
  font-weight: 500;
  color: #0e2460;
}
.our-team__content {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 2rem 4rem;
}
.team-member__image {
  margin-bottom: 30px;
}
.team-member__image img {
  width: 100%;
}
.team-member__name {
  margin-bottom: 5px;
  font-size: 18px;
  font-weight: 500;
}
.team-member__role {
  margin-bottom: 20px;
  font-size: 18px;
  font-weight: 400;
  color: #7a7a7a;
}
.team-member__description {
  margin-bottom: 20px;
  font-size: 18px;
  font-weight: 400;
  color: #7a7a7a;
}
</style>
