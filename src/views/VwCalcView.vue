<template>
    <p class=" text-4xl text-center mb-20">VW Calculator</p>
    <div class="flex flex-col sm:flex-row justify-around gap-4">
        <div class="mb-4">
            <div class="flex justify-between">
                <div class="flex justify-center gap-4 items-baseline">
                    <div class="flex items-center mb-4">
                        <input 
                            id="model-radio-1" 
                            type="radio" 
                            :value="null" 
                            name="model-radio" 
                            v-model="modelType" 
                            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
                        />
                        <label for="model-radio-1" class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300">General</label>
                    </div>
                    <div class="flex items-center">
                        <input checked id="model-radio-2" type="radio" :value="1" name="model-radio" v-model="modelType" @click="modelType = 1" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                        <label for="model-radio-2" class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300">ID.4 / BUZZ</label>
                    </div>
                </div>
                <div>
                    <button @click="clearForm">CLEAR</button>
                </div>
            </div>
            <FormInput inputId="invoiceAmount" v-if="!modelType">
                <template #label>invoice</template>
                <template #input-component>
                    <FormNumberInput v-model="invoiceAmount" inputId="invoiceAmount" />
                </template>
            </FormInput>
            <FormInput inputId="msrpAmount" v-if="!modelType">
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
            <FormInput inputId="destinationAmount" v-if="!modelType">
                <template #label>destination</template>
                <template #input-component>
                    <FormNumberInput v-model="destinationAmount" inputId="destinationAmount" />
                </template>
            </FormInput>
            <FormInput inputId="optionsAmount" v-if="modelType">
                <template #label>options</template>
                <template #input-component>
                    <FormNumberInput v-model="optionsAmount" inputId="optionsAmount" />
                </template>
            </FormInput>
            <FormInput inputId="paintAmount" v-if="modelType">
                <template #label>paint</template>
                <template #input-component>
                    <FormNumberInput v-model="paintAmount" inputId="paintAmount" />
                </template>
            </FormInput>
        </div>
        <div>
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
            <FormResult class="text-red-500 font-bold" v-if="!modelType">
                <template #label>
                    <span class="uppercase">fpa</span>
                </template>
                <template #value>{{ fpaTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold" v-if="modelType">
                <template #label>
                    <span class="uppercase">options</span>
                </template>
                <template #value>{{ optionsAmount }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold" v-if="modelType">
                <template #label>
                    <span class="uppercase">paint</span>
                </template>
                <template #value>{{ paintAmount }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold" v-if="modelType">
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
            <FormResult class="text-red-500 font-bold" v-if="!modelType">
                <template #label>
                    <span class="uppercase">trans credit</span>
                </template>
                <template #value>{{ transTotal }}</template>
            </FormResult>
            <FormResult class="text-red-500 font-bold" v-if="!modelType">
                <template #label>
                    <span class="uppercase">vpb</span>
                </template>
                <template #value>{{ vpbTotal }}</template>
            </FormResult>
        </div>
    </div>
</template>
<script setup>
import { computed, ref } from 'vue';
import FormInput from '@/components/FormInput.vue';
import FormNumberInput from '@/components/FormNumberInput.vue';
import FormResult from '@/components/FormResult.vue';

const invoiceAmount = ref(null)
const msrpAmount = ref(null)
const baseMsrpAmount = ref(null)
const destinationAmount = ref(null)
const optionsAmount = ref(null)
const paintAmount = ref(null)
const modelType = ref(null)

const total = computed(() => {
    // MSRP - Destination
    if(msrpAmount.value == null || destinationAmount.value == null) return null
    return Number(msrpAmount.value - destinationAmount.value).toFixed(2)
})

const dealerTradeTotal = computed(() => {
    // Invoice - Holdback
    if(invoiceAmount.value == null || holdbackTotal.value == null) return (0).toFixed(2)
    return Number(invoiceAmount.value - holdbackTotal.value).toFixed(2)
})

const holdbackTotal = computed(() => {
    // Other Base MSRP * 4.8% || Gen Base MSRP * 2%
    if(total.value == null) return (0).toFixed(2)
    if(modelType == null) {
        return Math.round(total.value * 0.02).toFixed(2)
    } else {
        return Math.round(total.value * 0.048).toFixed(2)
    }
})

const optionsTotal = computed(() => {
    // Options Amount * 2%
    if(modelType == null) return null
    if(optionsAmount > 0) {
        return Math.round(optionsAmount.value * 0.02).toFixed(2)
    }
})

const paintTotal = computed(() => {
    // Paint Amount * 7.8%
    if(modelType == null) return null
    if(paintAmount > 0) {
        return Math.round(paintAmount.value * 0.078).toFixed(2)
    }
})

const specialModelHoldbackTotal = computed(() => {
    if(modelType == null) return null
    const hb = Number(holdbackTotal.value)
    const opt = Number(optionsTotal.value)
    const pnt = Number(paintTotal.value)
    const ttl = hb + opt + pnt

    if(hb === 0 || opt === 0) return 0.00
    return Math.floor(ttl + 1).toFixed(2)
})

const fpaTotal = computed(() => {
    // Base MSRP * 1.5%
    if(baseMsrpAmount.value == null) return (0).toFixed(2)
    return Math.round(baseMsrpAmount.value * 0.015).toFixed(2)
})

const idmTotal = computed(() => {
    // Other Base MSRP * 2% || Gen Base MSRP * 0.8%
    if(baseMsrpAmount.value == null) return (0).toFixed(2)
    if(modelType == null) {
        return Math.round(baseMsrpAmount.value * 0.008).toFixed(2)
    } else {
        return Math.round(baseMsrpAmount.value * 0.02).toFixed(2)
    }
})

const transTotal = computed(() => {
    // Base MSRP * 1.35%
    // if value is under 50 (any hundred amount) round down,
    // else round up next dollar amount
    if(baseMsrpAmount.value == null) return (0).toFixed(2)
    const value = (baseMsrpAmount.value * 0.0135).toFixed(2)
    let val = Math.floor(Math.round(Number(value)))
    const dollarVal = val % 100
    if (dollarVal > 50) return (val + 1).toFixed(2)
    return (val).toFixed(2)
})

const vpbTotal = computed(() => {
    // Base MSRP * 1.9%
    if(baseMsrpAmount.value == null) return (0).toFixed(2)
    return Math.round(baseMsrpAmount.value * 0.019).toFixed(2)
})

const clearForm = () => {
    invoiceAmount = null
    msrpAmount = null
    baseMsrpAmount = null
    destinationAmount = null
    optionsAmount = null
    paintAmount = null
    modelType = null
}
</script>