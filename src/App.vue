<template>
  <NavBar/>
  <router-view class="container"/>
</template>

<script>
import NavBar from "./components/NavBar.vue";

export default({
  name: 'App',

  components: {
    NavBar,
  },
  watch:{
    $route(){
      this.$store.commit("onStart")
    }
  },
  mounted(){
    this.$store.commit("onStart")
  }
});
</script>


