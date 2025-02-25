<template>
  <div class="text-center border-4 border-amber-200 rounded-md drop-shadow-md">
    <div
      class="flex bg-amber-200 justify-start text-white font-bold p-2 text-xl gap-4"
      v-if="hasHeader"
    >
      <CogsIcon />Developer Note
    </div>
    <div class="p-4 bg-amber-100">
      <slot></slot>
    </div>
    <ContactMeLink
      class="flex bg-amber-200 justify-center text-white font-bold cursor-pointer"
      v-if="hasFooter"
    />
  </div>
</template>
<script setup>
import ContactMeLink from './ContactMeLink.vue'
import CogsIcon from 'vue-material-design-icons/Cogs.vue'

defineProps({
  hasHeader: {
    type: Boolean,
    default: true,
  },
  hasFooter: {
    type: Boolean,
    default: true,
  },
})
</script>
