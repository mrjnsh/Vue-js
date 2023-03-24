<template>
  <div
    class="Logout d-flex justify-space-around align-center flex-column flex-md-row fill-height"
  >
    <h1 class="text-h3 mt-5 mb-5">Logout</h1>
    <v-btn variant="outlined" color="primary" @click="doLogout"> Logout </v-btn>
  </div>
</template>

<script>
export default {
  name: "LogoutView",
  methods: {
    doLogout() {
      this.$store.commit("logout");
      this.$router.push("/login");
    },
  },
};
</script>
