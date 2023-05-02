<template>
  <div v-for="items in episodeInfo" v-if="episodeInfo">
    <a :href="items.external_urls.spotify" target="_blank">
      <p class="result-title-card">
        {{ items.name }}
      </p>
      <img
        v-if="items.images"
        class="result-image"
        :src="items.images[0].url"
      />
    </a>
  </div>
</template>

<script>
export default {
  props: ['episodeInfo']
}
</script>
