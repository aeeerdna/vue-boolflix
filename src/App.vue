<template>
  <div id="app">
    <div class="container">
      <div class="searchContainer">
        <input type="text" v-model="searchTitle" />
        <button @click="search">Search</button>
      </div>

      <div class="movieContainer" v-for="movie in movies" :key="movie.id">
        <p>
          {{ movie.title }}
        </p>

        <p>
          {{ movie.original_title }}
        </p>

        <p>
          {{ movie.original_language }}
        </p>

        <p>
          {{ movie.vote_average }}
        </p>
      </div>
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
      movies: [],
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
          if (response.status === 200) {
            this.movies = response.data.results;
          }
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
