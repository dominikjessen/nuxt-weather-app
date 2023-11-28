<script setup lang="ts">
defineProps<{
  weatherCode: number,
  className: string
}>()
</script>

<template>
  <div class="flex flex-col gap-4 items-center">
    <span>Weather Icon</span>
    <span>{{ weatherCode }}</span>
  </div>
</template>
