<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Bloggerz</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          -->
          <li class="nav-item active">
            <a class="nav-link" href="http://localhost:8080/posts">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              Dropdown
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="http://localhost:8080/posts/new">New Post</a>
              <a class="dropdown-item" href="#">Another action</a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>

    <div id="nav">
      <router-link to="/">Home</router-link>
      |
      <router-link to="/posts">All Posts</router-link>
      |
      <router-link to="/posts/new">New Post</router-link>
      |
      <!-- <router-link to="/signup">Signup</router-link> -->
      <router-link v-if="!isLoggedIn()" to="/signup">Signup</router-link>
      |
      <!-- <router-link to="/login">Login</router-link> -->
      <router-link v-if="!isLoggedIn()" to="/login">Login</router-link>
      |
      <!-- <router-link to="/logout">Logout</router-link> -->
      <router-link v-if="isLoggedIn()" to="/logout">Logout</router-link>
      |
    </div>

    <div class="container">
      <div v-if="flashMessage" v-on:click="flashMessage = ''" class="alert alert-success">{{ flashMessage }}</div>
      <router-view />
    </div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,300;1,800&display=swap");

body {
  font-family: "Montserrat", sans-serif !important;
  /* background-image: url("./assets/double-bubble-dark.png"); */
}

.navbar-brand {
  font-family: "Montserrat", sans-serif;
  font-size: 4em !important;
}
</style>

<script>
export default {
  data: function() {
    return {
      flashMessage: "",
    };
  },
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
