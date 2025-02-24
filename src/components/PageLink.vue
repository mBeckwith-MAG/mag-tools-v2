<template>
  <RouterLink
    :to="linkTo"
    class="bg-sky-300 p-4 drop-shadow-md hover:bg-sky-400 text-white rounded-b-lg"
    activeClass="bg-sky-600"
  >
    <slot></slot>
  </RouterLink>
</template>
<script setup>
defineProps({
  linkTo: String,
})
</script>
