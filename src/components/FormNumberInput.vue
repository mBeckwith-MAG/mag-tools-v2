<template>
    <input 
        type="number" 
        :id="inputId" 
        :placeholder="modelValue" 
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        class="border-b-1 border-b-gray-200 rounded-sm p-1 focus:border-sky-300 focus:outline-0 focus:border-b-2"
    />
</template>
<script setup>
defineProps({
    inputId: {
        type: String,
        require: true
    },
    modelValue: {
        type: Number
    }
})
const emit = defineEmits(['update:modelValue'])
</script>
<style scoped>
input[type="number"] {
    appearance: textfield;
    -webkit-appearance: textfield;
}
</style>