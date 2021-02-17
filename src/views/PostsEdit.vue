<template>
  <div class="posts-edit">
    <h1>Edit Post</h1>
    <form v-on:submit.prevent="updatePost()">
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" class="form-control" v-model="title" />
      Body:
      <input type="text" class="form-control" v-model="body" />
      Image:
      <input type="text" class="form-control" v-model="image" />
      <input type="submit" class="btn btn-primary" value="Update" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {},
      title: "",
      body: "",
      image: "",
      errors: [],
    };
  },
  created: function() {
    this.showPost();
  },
  methods: {
    showPost: function() {
      axios.get("api/posts/" + this.$route.params.id).then(response => {
        console.log(response.data);
        this.post = response.data;
        this.title = this.post.title;
        this.body = this.post.body;
        this.image = this.post.image;
      });
    },
    updatePost: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.image,
      };
      axios
        .patch("/api/posts/" + this.$route.params.id, params)
        // can also use this.recipe (saved variable) instead of $route.params.id
        .then(response => {
          console.log("posts update", response);
          this.$router.push("/posts");
        })
        .catch(error => {
          console.log("posts update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
