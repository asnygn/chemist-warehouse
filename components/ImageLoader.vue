<script setup>
defineProps([
  "imageUrl",
  "loadingStyle",
  "imageStyle",
  "backgroundImage",
  "backgroundImageStyle",
]);
</script>

<script>
export default {
  data() {
    return {
      isLoaded: false,
      isLoading: false,
    };
  },
  methods: {
    imageLoaded() {
      this.isLoaded = true;
      this.isLoading = false;
    },
  },
};
</script>

<template>
  <div v-if="backgroundImage">
    <section
      class="bg-image"
      v-bind:style="{ 'background-image': 'url(' + imageUrl + ')' }"
    >
      <slot></slot>
    </section>
  </div>
  <div v-else>
    <div v-show="!isLoaded" class="image-loading" :style="loadingStyle"></div>
    <img
      v-show="isLoaded"
      class="image"
      :src="imageUrl"
      @load="imageLoaded"
      :style="imageStyle"
    />
  </div>
</template>

<style scoped>
.bg-image {
  position: relative;
  background-color: #ddd;
  height: 600px;
}
.bg-image::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}

.image-loading {
  width: 100%;
  background-color: #ddd;
}
.image {
  width: 100%;
}

@media screen and (max-width: 780px) {
  .bg-image {
    height: 400px;
  }
}
</style>
