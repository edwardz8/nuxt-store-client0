<template>
  <div>
    <b-container>
      <b-card
        bg-variant="dark"
        text-variant="white"
        :title="$auth.$state.user.name"
        class="intro-card"
      >
        <b-card-text>
          Manage your settings and view your activity.
        </b-card-text>
        <b-card-group>
        <nuxt-link to="/">
          <b-button variant="primary">Home</b-button>
        </nuxt-link>
        <b-button variant="secondary" @click="logout">Logout</b-button>
        </b-card-group>
      </b-card>

      <div class="form-container">
      <b-card bg-variant="dark" text-variant="white">
        <b-form @submit.prevent="updateProfile">
          <b-form-group
            label="Email:"
            label-for="email">
            <b-form-input
              v-model="email"
              placeholder="Enter email"
            ></b-form-input>
          </b-form-group>

          <b-form-group label="Password:" label-for="password">
            <b-form-input
              v-model="password"
              placeholder="Enter password"
            ></b-form-input>
          </b-form-group>

          <b-button type="submit" variant="primary">Update</b-button>
        </b-form>

        <div style="margin-top: 1rem;">
          <p>Don't have an account? <nuxt-link to="/signup">Signup</nuxt-link></p>
        </div>
      </b-card>
    </div>
    </b-container>
  </div>
</template>

<script>
/* TODO: Add Update Profile Form. Logic already in-place */
export default {
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async updateProfile() {
      let data = {
        name: this.name,
        email: this.email,
        password: this.password,
      };
      try {
        let response = await this.$axios.$put("/api/auth/user", data);
        if (response.success) {
          this.name = "";
          this.email = "";
          this.password = "";
          await this.$auth.fetchUser();
        }
      } catch (err) {
        console.log(err);
      }
    },
    async logout() {
      await this.$auth.logout();
    },
  },
};
</script>
