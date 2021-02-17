<template>
  <div class="home">
    <h1>All Posts</h1>
    <div class="row">
      <div class="col-sm-3" v-for="post in posts" v-bind:key="post.id">
        <div class="card">
          <img v-bind:src="post.image" v-bind:alt="post.name" />
          <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <!-- <p class="card-text">With supporting text below as a natural lead-in to additional content.</p> -->
            <a class="btn btn-primary" v-bind:href="`/posts/${post.id}`">More info</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      posts: [],
    };
  },
  created: function() {
    this.indexPosts();
  },
  methods: {
    indexPosts: function() {
      axios.get("/api/posts").then(response => {
        console.log("posts index", response);
        this.posts = response.data;
      });
    },
  },
};
</script>
