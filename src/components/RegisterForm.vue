<template>
  <form @submit.prevent="registerUser">
    <BaseInput
      type="text"
      label="First Name"
      name="first_name"
      v-model="firstName"
      placeholder="Luke"
      class="mb-2"
    />
    <BaseInput
      type="text"
      label="Last Name"
      name="last_name"
      v-model="lastName"
      placeholder="Skywalker"
      class="mb-2"
    />
    <BaseInput
      type="email"
      label="Email"
      name="email"
      v-model="email"
      placeholder="luke@jedi.com"
      class="mb-2"
    />
    <BaseInput
      type="password"
      label="Password"
      name="password"
      v-model="password"
      class="mb-2"
    />
    <BaseInput
      type="password"
      label="Confirm Password"
      name="password-confirm"
      v-model="passwordConfirm"
      class="mb-4"
    />
    <BaseBtn type="submit" text="Register" />
    <FlashMessage :error="error" />
  </form>
</template>

<script>
import { getError } from "@/utils/helpers";
import BaseBtn from "@/components/BaseBtn";
import BaseInput from "@/components/BaseInput";
import AuthService from "@/services/AuthService";
import FlashMessage from "@/components/FlashMessage";

export default {
  name: "RegisterForm",
  components: {
    BaseBtn,
    BaseInput,
    FlashMessage,
  },
  data() {
    return {
      first_name: null,
      last_name: null,
      email: null,
      password: null,
      passwordConfirm: null,
      error: null,
      status: null,
      timezone: null
    };
  },
  methods: {
    registerUser() {
      this.error = null;
      const payload = {
        first_name: this.firstName,
        last_name: this.lastName,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirm,
        status: "enabled",
        timezone: "America/Chicago"
      };
      AuthService.registerUser(payload)
        .then(() => this.$router.push("/dashboard"))
        .catch((error) => (this.error = getError(error)));
    },
  },
};
</script>
