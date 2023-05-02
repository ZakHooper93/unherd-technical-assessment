<template>
  <div v-for="items in artistInfo" v-if="artistInfo">
    <a :href="items.external_urls.spotify" target="_blank">
      <p class="result-title-card zoom">
        {{ items.name }} {{ addGenre(items.genres[0]) }}
      </p>
      <img
        class="result-image zoom"
        :src="items.images[0].url"
      />
    </a>
  </div>
</template>

<script>
export default {
  props: ['artistInfo'],

  methods: {
    addGenre(genre) {
      if (genre) {
        return `- ${
          genre.charAt(0).toUpperCase() + genre.slice(1)
        }`
      }
    }
  }
}
</script>
