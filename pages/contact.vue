<script setup>
import axios from "axios";

const name = ref("");
const email = ref("");
const phone = ref("");
const message = ref("");

const formError = ref("");
const formSuccess = ref("");
const nameError = ref("");
const emailError = ref("");
const messageError = ref("");

const loading = ref(false);
const error = ref(false);
const data = ref(null);

async function submitContact() {
  const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i;

  if (!name.value) {
    nameError.value = "This field is required.";
  } else {
    nameError.value = "";
  }

  if (email.value && !regex.test(email.value)) {
    emailError.value = "Invalid email address.";
  } else {
    emailError.value = "";
  }

  if (!message.value) {
    messageError.value = "This field is required.";
  } else {
    messageError.value = "";
  }

  if (nameError.value || emailError.value || messageError.value) {
    return;
  }

  try {
    loading.value = true;
    const response = await axios.post(
      "https://api.chemistwarehouse.org/contacts/create",
      {
        name: name.value,
        email: email.value,
        phone: phone.value,
        message: message.value,
      }
    );
    data.value = response.data;
    formSuccess.value = "Form is successfully submit.";
    formError.value = "";
  } catch (err) {
    formSuccess.value = "";
    formError.value = err?.response?.data?.message;
    error.value = true;
  } finally {
    loading.value = false;
  }
}
</script>

<template>
  <!-- Main Header -->
  <MainHeader />
  <!-- Welcome Image -->
  <WelcomeImage
    title="Contact Us"
    description="Fusce id vehicula leo, nec accumsan lacus Praesent a dictum libero. Duis efficitur sem non nisi sodales"
    imageUrl="/image/about.jpg"
  />
  <section class="contact-us">
    <Container>
      <div class="contact-us__title">Contact Us</div>
      <form class="contact-form" @submit.prevent="submitContact">
        <div>
          <div class="form-error" v-if="formError">{{ formError }}</div>
          <div class="form-success" v-if="formSuccess">{{ formSuccess }}</div>
        </div>
        <div class="form-field">
          <label for="name">Name *</label>
          <input type="text" name="name" class="input-text" v-model="name" />
          <span class="form-field__error">{{ nameError }}</span>
        </div>
        <div class="form-group">
          <div class="form-field">
            <label for="email">Email</label>
            <input
              type="text"
              name="email"
              class="input-text"
              v-model="email"
            />
            <span class="form-field__error">{{ emailError }}</span>
          </div>
          <div class="form-field">
            <label for="phone">Phone</label>
            <input
              type="text"
              name="phone"
              class="input-text"
              v-model="phone"
            />
          </div>
        </div>
        <div class="form-field">
          <div>
            <label for="message">Message *</label>
            <textarea
              name="message"
              class="input-textarea"
              v-model="message"
            ></textarea>
            <span class="form-field__error">{{ messageError }}</span>
          </div>
        </div>
        <div class="form-actions">
          <button class="btn" type="submit">Submit</button>
        </div>
      </form>
    </Container>
  </section>
  <!-- Main Header -->
  <MainFooter />
</template>

<style scoped>
.contact-us {
  margin: 40px 0;
}
.contact-us__title {
  font-size: 30px;
  font-weight: 700;
  text-align: center;
}

.contact-form {
  margin: 20px auto;
  max-width: 600px;
}
.form-field {
  margin-bottom: 20px;
}
.form-field label {
  display: block;
  margin-bottom: 5px;
}
.form-field__error {
  color: red;
  font-size: 12px;
}
.form-group {
  display: flex;
  width: 100%;
  gap: 20px;
}
.form-group .form-field {
  flex: 1;
}
.input-text {
  padding: 12px 12px;
  width: 100%;
  background-color: #d9d9d9;
  border: none;
}
.input-textarea {
  padding: 12px 12px;
  width: 100%;
  height: 150px;
  background-color: #d9d9d9;
  border: none;
  resize: none;
}
.form-actions {
  text-align: right;
}
.btn {
  padding: 15px 40px;
  background-color: #1f3a81;
  color: #fff;
  border: none;
  cursor: pointer;
}

.form-error {
  margin-bottom: 20px;
  padding: 20px;
  font-size: 14px;
  background-color: #feecf0;
  color: #cc0f35;
}
.form-success {
  margin-bottom: 20px;
  padding: 20px;
  font-size: 14px;
  background-color: #effaf5;
  color: #257953;
}

input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
input:-webkit-autofill:active {
  -webkit-box-shadow: 0 0 0 30px #d9d9d9 inset !important;
}
</style>
