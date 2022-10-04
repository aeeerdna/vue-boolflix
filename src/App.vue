<template>
  <div id="app" class="container mt-2">
    <!-- Input e bottone cerca -->
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

    <!-- Container film e serie tv-->
    <div>
      <h3>Movies</h3>
      <MovieComponent v-for="movie in movies" :key="movie.id" :movie="movie" />

      <h3>Tv Series</h3>
      <TvSerieComponent
        v-for="tvSerie in tvSeries"
        :key="tvSerie.id"
        :tvSerie="tvSerie"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { apiKey } from "@/env.js";
import MovieComponent from "@/components/MovieComponent.vue";
import TvSerieComponent from "@/components/TvSerieComponent.vue";

export default {
  name: "App",
  data() {
    return {
      searchTitle: "",
      movies: [],
      tvSeries: [],
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

      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=${apiKey}&query=${searchTitle}&language=it-IT`
        )
        .then((response) => {
          console.log(response);
          if (response.status === 200) {
            this.tvSeries = response.data.results;
          }
        })
        .catch((error) => {
          console.log(error.message);
        });
    },
  },

  components: {
    MovieComponent,
    TvSerieComponent,
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap.scss";
</style>
