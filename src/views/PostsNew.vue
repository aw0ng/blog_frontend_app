<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div class="form-group">
      <label>Title:</label>
      <input type="text" class="form-control" v-model="newPostTitle" />
    </div>
    <div class="form-group">
      <label>Body:</label>
      <input type="email" class="form-control" v-model="newPostBody" />
    </div>
    <div class="form-group">
      <label>Image</label>
      <input type="password" class="form-control" v-model="newPostImage" />
    </div>
    <button v-on:click="createPosts()">Submit</button>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "New Post",
      newPostTitle: "",
      newPostBody: "",
      newPostImage: "",
    };
  },
  created: function() {},
  methods: {
    createPosts: function() {
      var params = {
        title: this.newPostTitle,
        body: this.newPostBody,
        image: this.newPostImage,
      };
      axios
        .post("/api/posts", params)
        .then(response => {
          console.log("posts create", response);
          this.$router.push("/posts");
          this.newPostTitle = "";
          this.newPostBody = "";
          this.newPostImage = "";
        })
        .catch(error => {
          console.log("posts create error", error.response);
        });
    },
  },
};
</script>
