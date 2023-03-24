<template>
  <div class="Home">
    <h1 class="text-center mb-5 mt-5">Home</h1>

    <v-alert
      v-model="alert"
      border="start"
      variant="tonal"
      color="#E57373"
      title="Articles"
    >
      <article v-for="article in articles" :key="article.value">
        <h3 class="mt-5">
          <router-link :to="`/article/${article.slug}`">{{
            article.title
          }}</router-link>
        </h3>
        <div>
          {{ article.description }}
          <router-link :to="`/article/${article.slug}`">+ more</router-link>
        </div>
      </article>
    </v-alert>
  </div>
</template>
<script>
// Components
export default {
  name: "HomeView",
  data() {
    let articles = localStorage.getItem("articles");
    articles = JSON.parse(articles);
    return {
      articles: articles,
      article: {},
    };
  },
};
</script>
