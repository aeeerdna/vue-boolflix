<template>
  <div id="app">
    <div class="container">
      <input type="text" v-model="searchTitle" />
      <button @click="search">Search</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { apiKey } from "@/env.js";
export default {
  name: "App",
  data() {
    return {
      searchTitle: "",
    };
  },

  methods: {
    search() {
      this.queryApi(this.searchTitle);
    },
    queryApi(searchTitle) {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&query=${searchTitle}&language=it-IT`
        )
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error.message);
        });
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap.scss";
</style>
