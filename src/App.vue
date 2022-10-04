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
        <p class="d-flex">
          Title:<span class="ms-2"> {{ movie.title }}</span>
        </p>

        <p class="d-flex">
          Original title:<span class="ms-2"> {{ movie.original_title }}</span>
        </p>

        <p class="d-flex">
          Language:
          <img
            class="languageFlag ms-2"
            :src="getFlag(movie.original_language)"
            :alt="movie.original_language"
            @error="fixImageError($event)"
          />
          <span class="ms-2"> {{ movie.original_language }}</span>
        </p>

        <p class="d-flex">
          Vote:<span class="ms-2"> {{ movie.vote_average }}</span>
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

    getFlag(language) {
      switch (language) {
        case "en": {
          language = "gb";
          break;
        }

        case "ja": {
          language = "jp";
          break;
        }

        case "da": {
          language = "dk";
          break;
        }

        case "cs": {
          language = "cz";
          break;
        }
      }

      return `https://flagicons.lipis.dev/flags/1x1/${language}.svg`;
    },

    fixImageError(event) {
      event.target.src = `https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRuboE0D1KX9nCaXspFfaDmec4xbX_P2SBXYw&usqp=CAU`;
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
  background-color: lightcoral;

  p {
    line-height: 1.6;
    margin: 0px;
    span {
      text-transform: uppercase;
      font-weight: bold;
    }
    .languageFlag {
      max-width: 15px;
    }
  }
}
</style>
