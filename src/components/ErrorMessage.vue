<template>
  <p class="error-card">
    {{ this.error }}
  </p>
</template>

<script>
export default {
  props: ['error']
}
</script>

<style scoped>
.error-card {
  width: 50%;
  max-width: 50%;
  background-color: rgba(28,28,30,.8);
  border-radius: 1.5rem;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  padding: 0.6rem 0.75rem;
  position: relative;
  font-size: medium;
  box-shadow: 0 0 10px red;
}
</style>
