<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <img v-if="status" v-bind:src="`https://http.cat/${status}`" v-on:click="status = ''" alt="" />
    <div class="form-group">
      <label>Title:</label>
      <input type="text" class="form-control" v-model="newPostTitle" />
    </div>
    <div class="form-group">
      <label>Body:</label>
      <input type="email" class="form-control" v-model="newPostBody" />
      <small>{{ 50 - newPostBody.length }} characters remaining</small>
      <div v-if="newPostBody.length > 50" :class="{ 'red-border': inputError }"></div>
    </div>
    <div class="form-group">
      <label>Image</label>
      <input type="password" class="form-control" v-model="newPostImage" />
    </div>
    <button v-on:click="createPost()">Submit</button>
  </div>
</template>

<style>
.red-border {
  border: 1px solid #f00;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "New Post",
      newPostTitle: "",
      newPostBody: "",
      newPostImage: "",
      status: "",
      inputError: true,
    };
  },
  created: function() {},
  methods: {
    toggleBorder: function(event) {
      this.inputError = true;
      event.target.classList.remove("red-border");
    },
    createPost: function() {
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
          this.status = error.response.status;
        });
    },
  },
};
</script>
