<template>
  <div class="movieContainer">
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
</template>

<script>
export default {
  name: "MovieComponent",
  props: {
    movie: Object,
  },
  methods: {
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

<style lang="scss" scoped>
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
