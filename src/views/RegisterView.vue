<template>
  <div
    class="register d-flex justify-space-around align-center flex-column flex-md-row fill-height"
  >
    <h1 class="text-h3 mt-5 mb-5">Register</h1>
    <v-sheet width="300" class="mx-auto">
      <v-form fast-fail @submit.prevent="doRegister">
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

        <v-text-field
          label="Repeat Password"
          v-model="password2"
        ></v-text-field>
        <div v-if="password2E">
          {{ password2EM }}
        </div>

        <v-btn
          type="submit"
          block
          class="mt-2"
          variant="outlined"
          color="#B71C1C"
          @click="doRegister"
          >Register</v-btn
        >
      </v-form>
    </v-sheet>
  </div>
</template>

<script>
export default {
  name: "RegisterView",
  data() {
    return {
      username: "",
      password: "",
      password2: "",
      usernameE: null,
      passwordE: null,
      password2E: null,
      usernameEM: null,
      passwordEM: null,
      password2EM: null,
    };
  },
  methods: {
    doRegister() {
      let access = true;
      //username
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
//password
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
      //confirm password
      if (this.password2.length < 8) {
        access = false
        this.password2E = true
        if (this.password2.length == 0) {
          this.password2EM = "Repeat password required."
        } else {
          this.password2EM = "Repeat password must be at least 8 characters long."
        }
      } else {
        this.password2E = false
        this.password2EM = ''
      }
      if (this.password != this.password2) {
        access = false
        this.passwordE = true
        this.password2E = true
        this.passwordEM = "Passwords are't same."
      } else {
        if (!this.passwordEM && !this.password2EM) {
          this.passwordEM = ""
        }
      }
      

      if (access) {
        this.$store.commit("/login", `${this.username}:${this.password}`);
        this.$router.push("/profile");
      }
    },
  },
};
</script>
