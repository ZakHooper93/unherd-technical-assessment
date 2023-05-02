<template>
  <div v-for="items in albumInfo" v-if="albumInfo">
    <a :href="items.external_urls.spotify" target="_blank">
      <p class="result-title-card zoom">
        {{ items.name }} {{ addDate(items.release_date) }}
      </p>
      <img
        v-if="items.images"
        class="result-image zoom"
        :src="items.images[0].url"
      />
    </a>
  </div>
</template>

<script>
export default {
  props: ['albumInfo'],

  methods: {
    addDate(releaseDate) {
      if (releaseDate) {
        return `- ${releaseDate.split('-')[0]} `
      }
    }
  }
}
</script>