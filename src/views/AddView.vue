<template>
  <div class="Add ma-9">
    <v-form @submit.prevent="doAdd">
      <v-text-field
        v-model="title"
        class="ml-3 w-25"
        label="Title :"
      ></v-text-field>
      <v-textarea v-model="description" label="Description :"></v-textarea>
      <v-textarea v-model="content" label="Content :"></v-textarea>
      <v-row justify="center">
        <v-col cols="auto">
          <v-btn type="submit"  height="72" min-width="164" color="#EF9A9A">
            Add Article
          </v-btn>
        </v-col>
      </v-row>
    </v-form>
  </div>
</template>
<script>
// Components
export default {
  name: "AddView",
  data() {
    let articles = localStorage.getItem("articles");
    articles = JSON.parse(articles);
    return {
      articles: articles,
      title: "",
      description: "",
      content: "",
    };
  },
  methods: {
    doAdd() {
      let article = {
        title: this.title,
        slug: this.title.replaceAll(" ", "-").toLowerCase(),
        description: this.description,
        content: this.content,
      };
      this.articles.push(article);
      let database = JSON.stringify(this.articles);
      localStorage.setItem("articles", database);
      this.$router.push(`/article/${article.slug}`);
    },
  },
};
</script>

