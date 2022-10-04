<template>
  <!-- bandiera lingua -->
  <img
    class="languageFlag ms-2"
    :src="getFlag(language)"
    :alt="language"
    @error="fixImageError($event)"
  />
</template>

<script>
export default {
  name: "FlagComponent",
  props: {
    language: String,
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
.languageFlag {
  max-width: 15px;
}
</style>
