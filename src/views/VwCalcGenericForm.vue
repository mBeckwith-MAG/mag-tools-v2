<template>
    <div class="flex flex-col sm:flex-row justify-around gap-4">
        <div>
            <FormInput inputId="invoiceAmount">
                <template #label>invoice</template>
                <template #input-component>
                    <FormNumberInput v-model="invoiceAmount" inputId="invoiceAmount" />
                </template>
            </FormInput>
            <FormInput inputId="msrpAmount">
                <template #label>msrp</template>
                <template #input-component>
                    <FormNumberInput v-model="msrpAmount" inputId="msrpAmount" />
                </template>
            </FormInput>
            <FormInput inputId="baseMsrpAmount">
                <template #label>base msrp</template>
                <template #input-component>
                    <FormNumberInput v-model="baseMsrpAmount" inputId="baseMsrpAmount" />
                </template>
            </FormInput>
            <FormInput inputId="destinationAmount">
                <template #label>destination</template>
                <template #input-component>
                    <FormNumberInput v-model="destinationAmount" inputId="destinationAmount" />
                </template>
            </FormInput>
        </div>
        <div class="mt-4">
            <FormResult class="text-red-500 font-bold mb-8">
                <template #label>
                <span class="uppercase">dealer trade total</span>
                </template>
                <template #value>{{ dealerTradeTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">holdback</span>
                </template>
                <template #value>{{ holdbackTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">fpa</span>
                </template>
                <template #value>{{ fpaTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">idm / adv assist</span>
                </template>
                <template #value>{{ idmTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">trans credit</span>
                </template>
                <template #value>{{ transTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold">
                <template #label>
                <span class="uppercase">vpb</span>
                </template>
                <template #value>{{ vpbTotal }}</template>
            </FormResult>
        </div>
    </div>
    
    
</template>
<script setup>
import { ref, computed } from 'vue'

import FormInput from'@/components/FormInput.vue'
import FormNumberInput from'@/components/FormNumberInput.vue'
import FormResult from'@/components/FormResult.vue'

const invoiceAmount = ref(null)
const msrpAmount = ref(null)
const baseMsrpAmount = ref(null)
const destinationAmount = ref(null)

const dealerTradeTotal = computed(() => {
    return (0).toFixed(2)
})
const holdbackTotal = computed(() => {
    return (0).toFixed(2)
})
const fpaTotal = computed(() => {
    return (0).toFixed(2)
})
const idmTotal = computed(() => {
    return (0).toFixed(2)
})
const transTotal = computed(() => {
    return (0).toFixed(2)
})
const vpbTotal = computed(() => {
    return (0).toFixed(2)
})
</script>