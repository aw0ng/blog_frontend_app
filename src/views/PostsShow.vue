<template>
  <div>
    <h1>{{ post.title }}</h1>
    <img v-bind:src="post.image" v-bind:alt="post.name" />
    <p>{{ post.body }}</p>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {},
    };
  },
  created: function() {},
  methods: {
    showPosts: function() {
      //  + this.$route.params.id
      axios.get("/api/posts/1").then(response => {
        // "posts show",
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
