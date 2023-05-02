<template>
  <div v-for="items in audiobookInfo" v-if="audiobookInfo">
    <a :href="items.external_urls.spotify" target="_blank">
      <p class="result-title-card zoom">
        {{ items.name }} - {{ items.authors[0].name }} -
        Narrated by {{ items.narrators[0].name }}
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
  props: ['audiobookInfo']
}
</script>
