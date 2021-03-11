<template>
<div class="container-signup">
    <b-card bg-variant="dark" text-variant="white" title="Login to Account" class="intro-card">
      <b-card-text>
        Welcome to Sweaters, Skates and Sticks. The best card trading platform for sports fans.
      </b-card-text>
      <nuxt-link to="/">
      <b-button variant="primary">Home</b-button>
      </nuxt-link>
    </b-card>

    <div class="form-container">
      <b-card bg-variant="dark" text-variant="white">
        <b-form @submit.prevent="login">
          <b-form-group
            label="Email:"
            label-for="email">
            <b-form-input
              v-model="email"
              placeholder="Enter email"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group label="Password:" label-for="password">
            <b-form-input
              v-model="password"
              placeholder="Enter password"
              required
            ></b-form-input>
          </b-form-group>

          <b-button type="submit" variant="primary">Login</b-button>
        </b-form>

        <div style="margin-top: 1rem;">
          <p>Don't have an account? <nuxt-link to="/signup">Signup</nuxt-link></p>
        </div>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  middleware: "auth",
  auth: "guest",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    async login() {
      try {
        this.$auth.loginWith("local", {
          data: {
            email: this.email,
            password: this.password
          }
        });

        this.$router.push("/");

      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>

<style>
.container-signup {
  margin: 0 auto;
  display: flex;
  height: 100vh;
  flex-direction: column;
  margin-left: 1rem;
  margin-right: 1rem;
}
.intro-card {
  margin-top: 1rem;
  margin-bottom: 1rem;
}
.form-container {
  margin-top: 1rem;
}
</style>