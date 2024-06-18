<script>
import axios from "axios";
import { format } from "date-fns";

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
        const response = await axios.post("https://cw-api.zino.tech/csr/list");
        this.data = response.data;
      } catch (err) {
        this.error = true;
      } finally {
        this.loading = false;
      }
    },
    timelineDate(date) {
      if (date) {
        return format(new Date(date), "MMMM yyyy");
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
    title="CSR"
    description="Fusce id vehicula leo, nec accumsan lacus. <br /> Praesent a dictum libero. Duis efficitur sem <br /> non nisi sodales"
    imageUrl="/image/csr.jpg"
    v-if="data"
  />
  <!-- CSR Timeline -->
  <section class="csr-timeline" v-if="data && data?.list">
    <Container>
      <div class="timeline" v-for="item in data?.list">
        <div class="timeline__date">
          <!-- {{ item.date }} -->
          {{ timelineDate(item.date) }}
        </div>
        <div class="timeline__content-layout">
          <div class="timeline__title">
            {{ item.title }}
          </div>
          <div class="timeline__description">
            {{ item.shortDescription }}
          </div>
        </div>
        <div class="timeline__image">
          <img :src="item.coverImage" />
        </div>
      </div>
    </Container>
  </section>
  <!-- Main Footer -->
  <MainFooter v-if="data" />
</template>

<style scoped>
.csr-timeline {
  padding: 100px 0;
}

.timeline {
  display: flex;
  margin-bottom: 60px;
}
.timeline__date {
  min-width: 200px;
  font-size: 30px;
  font-weight: 500;
}
.timeline__title {
  min-width: 220px;
  margin-bottom: 40px;
  font-size: 25px;
}
.timeline__description {
  font-size: 18px;
  color: #7a7a7a;
}
.timeline__content-layout {
  padding-left: 80px;
  padding-right: 60px;
  border-left: 2px solid #e2e2e2;
}
</style>
