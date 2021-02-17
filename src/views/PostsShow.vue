<template>
  <div class="posts-show">
    <h2>{{ post.title }}</h2>
    <p>{{ post.body }}</p>
    <p>Author: {{ post.is_owner }}</p>
    <img v-bind:src="post.url" v-bind:alt="post.title" />
    <router-link v-if="post.is_owner" v-bind:to="`/posts/${post.id}/edit`">Edit post</router-link>
    <p>
      <router-link to="/posts">Back to all posts</router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      post: {},
    };
  },
  created: function() {
    axios.get("/api/posts/" + this.$route.params.id).then(response => {
      console.log("posts show", response);
      this.post = response.data;
    });
  },
  methods: {},
};
</script>
