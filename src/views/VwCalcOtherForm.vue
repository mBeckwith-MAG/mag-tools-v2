<template>
    <div class="flex flex-col sm:flex-row justify-around gap-4">
        <div>
            <FormInput inputId="baseMsrpAmount">
                <template #label>base msrp</template>
                <template #input-component>
                    <FormNumberInput v-model="baseMsrpAmount" inputId="baseMsrpAmount" />
                </template>
            </FormInput>
            <FormInput inputId="optionsAmount">
                <template #label>options</template>
                <template #input-component>
                <FormNumberInput v-model="optionsAmount" inputId="optionsAmount" />
                </template>
            </FormInput>
            <FormInput inputId="paintAmount">
                <template #label>paint</template>
                <template #input-component>
                <FormNumberInput v-model="paintAmount" inputId="paintAmount" />
                </template>
            </FormInput>
        </div>
        <div class="mt-4">
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">holdback</span>
                </template>
                <template #value>{{ holdbackTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">options</span>
                </template>
                <template #value>{{ optionsAmount }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">paint</span>
                </template>
                <template #value>{{ paintAmount }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">total holdback</span>
                </template>
                <template #value>{{ specialModelHoldbackTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">idm / adv assist</span>
                </template>
                <template #value>{{ idmTotal }}</template>
            </FormResult>
        </div>
    </div>
</template>
<script setup>
import { ref, computed } from 'vue'
import FormInput from '@/components/FormInput.vue'
import FormNumberInput from '@/components/FormNumberInput.vue'
import FormResult from '@/components/FormResult.vue'

const baseMsrpAmount = ref(null)
const optionsAmount = ref(null)
const paintAmount = ref(null)

const holdbackTotal = computed(() => {
    return (0).toFixed(2)
})
const optionsTotal = computed(() => {
    return (0).toFixed(2)
})
const paintTotal = computed(() => {
    return (0).toFixed(2)
})
const specialModelHoldbackTotal = computed(() => {
    return (0).toFixed(2)
})
const idmTotal = computed(() => {
    return (0).toFixed(2)
})
</script>