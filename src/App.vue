<template>
  <div id="app">ciao</div>
</template>

<script>
import axios from "axios";
import { apiKey } from "@/env.js";
export default {
  name: "App",
  mounted() {
    this.queryApi("8 mile");
  },
  methods: {
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
