<script setup>
defineProps(["title", "description", "imageUrl"]);
</script>

<template>
  <ImageLoader
    :imageUrl="imageUrl"
    :backgroundImage="true"
    backgroundImageStyle="height: 600px"
  >
    <Container class="container">
      <div class="welcome__body">
        <div class="welcome__text1">
          <p>{{ title }}</p>
        </div>
        <div class="welcome__text2" v-html="description"></div>
      </div>
    </Container>
  </ImageLoader>
</template>

<style scoped>
.container {
  position: relative;
  height: 100%;
}

.welcome__body {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

.welcome__text1 {
  margin-bottom: 20px;
  font-size: 22px;
  font-weight: 500;
  color: #fff;
}

.welcome__text2 {
  font-size: 30px;
  font-weight: 900;
  color: #fff;
}
</style>
