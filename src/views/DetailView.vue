<template>
  <div class="Detail">
    <h1 class="text-center mb-5 mt-5">Detail</h1>

    <v-alert
      v-model="alert"
      border="start"
      variant="tonal"
      color="#E57373"
      title="Articles"
    >
      <article>
        <h3 class="mt-5">
          {{ article.title }}
        </h3>
        <div>
          {{ article.content }}
        </div>
      </article>
    </v-alert>
    <div v-if="$store.state.isAuthenticated">
      <v-btn class="ma-5" @click="edit = !edit">Edit</v-btn>
      <v-btn class="ma-5" @click="doRemove">Remove</v-btn>
      <v-form @submit.prevent="doEdit" v-if="edit">
        <v-text-field
          v-model="title"
          class="ml-3 w-25"
          label="Title :"
        ></v-text-field>
        <v-textarea v-model="description" label="Description :"></v-textarea>
        <v-textarea v-model="content" label="Content :"></v-textarea>
        <v-row justify="center">
          <v-col cols="auto">
            <v-btn type="submit" height="72" min-width="164" color="#EF9A9A">
              Edit Article
            </v-btn>
          </v-col>
        </v-row>
      </v-form>
    </div>
  </div>
</template>
<script>
// Components
export default {
  name: "DetailView",
  data() {
    let articles = localStorage.getItem("articles");
    articles = JSON.parse(articles);
    let article = articles.find(
      (article) => article.slug == this.$route.params.slug
    );
    return {
      articles: articles,
      article: article,
      title: article.title,
      description: article.description,
      content: article.content,
      edit: false,
    };
  },
  methods: {
    doEdit() {
      let index = this.articles.findIndex(
        (article) => article.slug == this.$route.params.slug
      );
      this.articles[index] = {
        title: this.title,
        slug: this.title.replaceAll(" ", "-").toLowerCase(),
        description: this.description,
        content: this.content,
      };
      let database = JSON.stringify(this.articles);
      localStorage.setItem("articles", database);
      this.article = this.articles[index];
      this.$router.push(`/article/${this.articles[index].slug}`);
    },

    doRemove() {
      let index = this.articles.findIndex(
        (article) => article.slug == this.$route.params.slug
      );
      this.articles.splice(index, 1);

      let database = JSON.stringify(this.articles);
      localStorage.setItem("articles", database);
      this.$router.push("/");
    },
  },
};
</script>
