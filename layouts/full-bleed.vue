<script setup lang="ts">
defineProps<{
  image?: string
}>()
</script>

<template>
  <div class="full-bleed">
    <BaseImg :src="image" class="full-bleed-img" alt="" />
    <div class="full-bleed-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.full-bleed {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: var(--paper);
}

.full-bleed-img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  max-width: none;
  max-height: none;
  object-fit: cover;
  display: block;
}

.full-bleed-content {
  position: relative;
  z-index: 1;
  width: 100%;
  height: 100%;
}
</style>
