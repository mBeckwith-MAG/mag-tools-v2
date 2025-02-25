<template>
    <div class="flex items-center">
        <input
            type="radio"
            :id="radioId"
            :name="groupName"
            :value="radioVal"
            :checked="isChecked"
            @change="$emit('update:modelValue', value)"
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
        />
        <label :for="radioId" class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300 border-1 border-sky-300 p-3 checked:bg-sky-300 rounded-md">
            <slot></slot>    
        </label>
    </div>
</template>
<script setup>
defineProps({
    radioId: {
        type: String,
        required: true
    },
    groupName: {
        type: String,
        required: true
    },
    radioVal: {
        type: Boolean,
        required: true
    },
    isChecked: {
        type: Boolean,
        default: false
    },
    modelValue: {
        type: Boolean
    }
})
defineEmits(['update:modelValue'])
</script>
<style scoped>
input[type="radio"] {
    display: none
}
input[type="radio"]:checked + label {
    background-color: #49a5ca;
    color: #fff;
}
</style>