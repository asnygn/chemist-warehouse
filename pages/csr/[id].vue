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
    async fetchData(id) {
      this.loading = true;
      try {
        const response = await axios.post(
          "https://api.chemistwarehouse.org/csr/list",
          {
            id,
          }
        );
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
    const route = useRoute();
    this.fetchData(route.params.id);
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
    :imageUrl="data?.list?.[0]?.coverImage"
    v-if="data"
  />
  <!-- CSR Timeline -->
  <section class="csr-timeline" v-if="data && data?.list">
    <Container>
      <div class="timeline" v-for="item in data?.list">
        <div class="timeline__date">
          {{ timelineDate(item.date) }}
        </div>
        <div class="timeline__content-layout">
          <div class="timeline__text-group">
            <div class="timeline__title">
              {{ item.title }}
            </div>
            <div class="timeline__description">
              {{ item.shortDescription }}
            </div>
          </div>
          <div class="timeline__image" v-for="item2 in data?.list?.[0]?.images">
            <img :src="item2.image" />
          </div>
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
.timeline__text-group {
  padding-left: 80px;
  padding-bottom: 40px;
  margin-bottom: 40px;
  border-left: 2px solid #e2e2e2;
}
.timeline__image {
  padding-left: 80px;
  margin-bottom: 40px;
}
.timeline__image img {
  width: 100%;
}

@media screen and (max-width: 980px) {
  .timeline__title {
    margin-bottom: 20px;
  }
}

@media screen and (max-width: 780px) {
  .timeline {
    display: block;
    margin-bottom: 40px;
  }
  .timeline__date {
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 2px solid #e2e2e2;
  }
  .timeline__text-group {
    padding-left: 0;
    padding-right: 0;
    padding-bottom: 0;
    border: none;
  }
  .timeline__image {
    padding-left: 0;
    padding-right: 0;
  }
}
</style>
