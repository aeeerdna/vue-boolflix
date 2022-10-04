<template>
  <div id="app">
    <div class="container mt-2">
      <div class="searchContainer d-flex">
        <input
          class=""
          type="text"
          placeholder="Movie title"
          v-model="searchTitle"
        />
        <button class="btn btn-primary btn-sm ms-2" @click="search">
          Search
        </button>
      </div>

      <div class="movieContainer" v-for="movie in movies" :key="movie.id">
        <p>
          Title: <span>{{ movie.title }}</span>
        </p>

        <p>
          Original title: <span>{{ movie.original_title }}</span>
        </p>

        <p>
          Language: <span>{{ movie.original_language }}</span>
        </p>

        <p>
          Vote: <span>{{ movie.vote_average }}</span>
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

.movieContainer {
  margin-top: 20px;
  border: 2px solid black;
  padding: 10px;

  p {
    line-height: 1.6;
    margin: 0px;
    span {
      text-transform: uppercase;
      font-weight: bold;
    }
  }
}
</style>
