<template>
  <div
    class="login d-flex justify-space-around align-center flex-column flex-md-row fill-height"
  >
    <h1 class="text-h3 mt-5 mb-5">Login</h1>
    <v-sheet width="300" class="mx-auto">
      <v-form fast-fail @submit.prevent="doLogin">
        <v-text-field
          label="Username"
          id="usernameInput"
          v-model="username"
        ></v-text-field>
        <div v-if="usernameE">
          {{ usernameEM }}
        </div>

        <v-text-field label="Password" v-model="password"></v-text-field>
        <div v-if="passwordE">
          {{ passwordEM }}
        </div>

        <v-btn
          type="submit"
          block
          class="mt-2"
          variant="outlined"
          color="#B71C1C"
          @click="doLogin"
          >Login</v-btn
        >
      </v-form>
    </v-sheet>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  data() {
    return {
      username: "",
      password: "",
      usernameE: null,
      passwordE: null,
      usernameEM: null,
      passwordEM: null,
    };
  },
  methods: {
    doLogin() {
      let access = true;
      if (this.username.length < 5) {
        access = false;
        this.usernameE = true;
        if (this.username.length == 0) {
          this.usernameEM = "Username required *";
        } else {
          this.usernameEM = "Username must be at least 5 characters long.";
        }
      } else {
        this.usernameE = false;
        this.usernameEM = "";
      }
      if (this.password.length < 8) {
        access = false;
        this.passwordE = true;
        if (this.password.length == 0) {
          this.passwordEM = "Password required *";
        } else {
          this.passwordEM = "Password must be at least 8 characters long.";
        }
      } else {
        this.passwordE = false;
        this.passwordEM = "";
      }

      if (access) {
        this.$store.commit("login", `${this.username}:${this.password}`);
        this.$router.push("/profile");
      }
    },
  },
};
</script>

<style>
div {
  color: #d33737;
}
</style>
