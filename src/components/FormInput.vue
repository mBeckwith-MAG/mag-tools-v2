<template>
    <div class="flex justify-between mb-3 gap-10 items-center">
        <label :for="inputId" class="uppercase">
            <slot name="label"></slot>
        </label>
        <slot name="input-component"></slot>
    </div>
</template>
<script setup>
defineProps({
    inputId: {
        type: String,
        require: true
    },
})
const emit = defineEmits(['update:modelValue'])
</script>
