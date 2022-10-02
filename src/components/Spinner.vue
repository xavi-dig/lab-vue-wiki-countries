<template>
  <div class="d-flex flex-column align-items-center justify-content-center">
    <div class="spinner-border mb-4 text-primary" role="status"></div>
    <p>{{ text }}</p>
  </div>
</template>

<script setup>
defineProps({
  text: {
    type: String,
  },
});
</script>

<style></style>
