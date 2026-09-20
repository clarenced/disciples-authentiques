<script setup lang="ts">
defineProps<{
  heading?: string
}>()
</script>

<template>
  <SceneBackground>
    <div class="verse-slide">
      <h1 class="verse-title">{{ heading }}</h1>
      <div class="verse-body">
        <slot />
      </div>
    </div>
  </SceneBackground>
</template>
