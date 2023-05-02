<template>
  <div v-for="items in showInfo" v-if="showInfo">
    <a :href="items.external_urls.spotify" target="_blank">
      <p class="result-title-card">
        {{ items.name }}
      </p>
    </a>
  </div>
</template>

<script>
export default {
  props: ['showInfo']
}
</script>
