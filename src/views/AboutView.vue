<template>
  <DevMessage :has-header="false" :has-footer="false">
    <div class="flex justify-center gap-2 items-baseline pb-4">
      <span class="text-xs">Created By</span>
      <span class="text-xl">Matthew Beckwith</span>
    </div>
    <small>February 20, 2024 - Current</small>
  </DevMessage>
</template>
<script setup>
import DevMessage from '@/components/DevMessage.vue'
</script>
