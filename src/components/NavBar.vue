<template>
  <div class="NavBar mb-0">
    <v-toolbar density="compact" color="#FF8A80">
      <router-link to="/"><v-btn>Home</v-btn></router-link>
      <router-link to="/about"><v-btn>About</v-btn></router-link>
      <router-link to="/profile" v-if="$store.state.isAuthenticated"
        ><v-btn>Profile</v-btn></router-link
      >
      <router-link to="/add" v-if="$store.state.isAuthenticated"
        ><v-btn>Write an article</v-btn></router-link
      >
      <router-link to="/login" v-if="!$store.state.isAuthenticated"
        ><v-btn>Login</v-btn></router-link
      >
      <router-link to="/logout" v-if="$store.state.isAuthenticated"
        ><v-btn>Logout</v-btn></router-link
      >
      <router-link to="/register" v-if="$store.state.isAuthenticated"
        ><v-btn>Register</v-btn></router-link
      >
    </v-toolbar>
  </div>
</template>

<script>
export default {
  name: "NavBar",
};
</script>

<style>
a {
  text-decoration: none;
  font-family: sans-serif;
  color: #040202;
}
</style>
