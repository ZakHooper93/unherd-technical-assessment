<template>
  <div v-for="items in trackInfo" v-if="trackInfo">
    <a :href="items.external_urls.spotify" target="_blank">
      <p class="result-title-card zoom">
        {{ items.name }} - {{ items.artists[0].name }} -
        {{ items.album.name }}
      </p>
      <!-- I'd like to make a seperate API call using the album ID to place related album artwork -->
      <!-- <img
        v-if="items.images"
        class="result-image zoom"
        :src="items.images[0].url"
      /> -->
    </a>
  </div>
</template>

<script>
export default {
  props: ['trackInfo']
}
</script>

<style scoped>
.result-title-card {
  margin-top: 20px;
}
</style>
