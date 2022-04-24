<script setup lang="ts">
defineProps<{ err: any }>()
</script>

<template>
  <div>
    <div>エラーが発生しました</div>
    <div>{{ err }}</div>
  </div>
</template>
