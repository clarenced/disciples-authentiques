<script setup lang="ts">
const props = defineProps<{
  src: string
}>()

const resolved = import.meta.env.BASE_URL.replace(/\/$/, '') + props.src
</script>

<template>
  <img :src="resolved" />
</template>
