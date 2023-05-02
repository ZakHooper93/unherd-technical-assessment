<template>
  <div v-for="items in playlistInfo" v-if="playlistInfo">
    <a :href="items.external_urls.spotify" target="_blank">
      <p class="result-title-card zoom">
        {{ items.name }}
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
  props: ['playlistInfo']
}
</script>
