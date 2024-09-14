<script setup>
defineProps(["imageUrl"]);
</script>

<script>
export default {
  methods: {
    scrollToElement() {
      const element = document.getElementById("contact-us");
      element.scrollIntoView({ behavior: "smooth", alignToTop: true });
    },
  },
};
</script>

<template>
  <ImageLoader :imageUrl="imageUrl" :backgroundImage="true">
    <Container class="container">
      <div class="contact">
        <div class="contact__text">
          <p>Have any inquiries? Please feel free to contact us anytime.</p>
        </div>
        <div class="contact__link">
          <a @click="scrollToElement">Contact us now</a>
        </div>
      </div>
    </Container>
  </ImageLoader>
</template>

<style scoped>
.container {
  position: relative;
  height: 100%;
}

.contact {
  position: absolute;
  top: 50%;
  transform: translate(0%, -50%);
  padding: 20px;
  max-width: 320px;
  background-color: #1f3a81;
}
.contact__text {
  margin-bottom: 20px;
  color: #fff;
  line-height: 1.5;
}
.contact__link {
  text-align: center;
}
.contact__link a {
  padding: 10px 20px;
  background-color: #56c512;
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
</style>
