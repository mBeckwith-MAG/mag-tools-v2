<template>
  <p class="text-4xl text-center mb-20">VW Calculator</p>
  <p>{{ modelType }}</p>
  <div class="flex justify-between">
    <div class="flex justify-center gap-4 items-baseline">
      <div class="flex items-center mb-4">
        <FormRadio radioId="model-radio-1" groupName="model-radio" :radioVal="false" v-model="modelType" isChecked>Generic</FormRadio>
        <FormRadio radioId="model-radio-2" groupName="model-radio" :radioVal="true" v-model="modelType">ID.4 / BUZZ</FormRadio>
      </div>
    </div>
  </div>
  <div v-if="modelType">
    <VwCalcOtherForm />
  </div>
  <div v-else>
    <VwCalcGenericForm />
  </div>
</template>
<script setup>
import { computed, ref } from 'vue'
import VwCalcGenericForm from '@/views/VwCalcGenericForm.vue'
import VwCalcOtherForm from '@/views/VwCalcOtherForm.vue'
import FormRadio from '@/components/FormRadio.vue'

const modelType = ref(false)

// const total = computed(() => {
//   // MSRP - Destination
//   if (msrpAmount.value == null || destinationAmount.value == null) return (0).toFixed(2)
//   return Number(msrpAmount.value - destinationAmount.value).toFixed(2)
// })

// const dealerTradeTotal = computed(() => {
//   // Invoice - Holdback
//   if (invoiceAmount.value == null || holdbackTotal.value == null) return (0).toFixed(2)
//   return Number(invoiceAmount.value - holdbackTotal.value).toFixed(2)
// })

// const holdbackTotal = computed(() => {
//   // Other Base MSRP * 4.8% || Gen Base MSRP * 2%
//   if (total.value == null) return (0).toFixed(2)
//   if (modelType.value == false) {
//     return Math.round(total.value * 0.02).toFixed(2)
//   } else {
//     return Math.round(total.value * 0.048).toFixed(2)
//   }
// })

// const optionsTotal = computed(() => {
//   // Options Amount * 2%
//   if (modelType.value == false) return (0).toFixed(2)
//   if (optionsAmount.value > 0) {
//     return Math.round(optionsAmount.value * 0.02).toFixed(2)
//   }
// })

// const paintTotal = computed(() => {
//   // Paint Amount * 7.8%
//   if (modelType.value == false) return (0).toFixed(2)
//   if (paintAmount.value > 0) {
//     return Math.round(paintAmount.value * 0.078).toFixed(2)
//   }
// })

// const specialModelHoldbackTotal = computed(() => {
//   if (modelType.value == false) return (0).toFixed(2)
//   const hb = Number(holdbackTotal.value)
//   const opt = Number(optionsTotal.value)
//   const pnt = Number(paintTotal.value)
//   const ttl = hb + opt + pnt

//   if (hb === 0 || opt === 0) return (0).toFixed(2)
//   return Math.floor(ttl + 1).toFixed(2)
// })

// const fpaTotal = computed(() => {
//   // Base MSRP * 1.5%
//   if (baseMsrpAmount.value == null) return (0).toFixed(2)
//   return Math.round(baseMsrpAmount.value * 0.015).toFixed(2)
// })

// const idmTotal = computed(() => {
//   // Other Base MSRP * 2% || Gen Base MSRP * 0.8%
//   if (baseMsrpAmount.value == null) return (0).toFixed(2)
//   if (modelType.value == null) {
//     return Math.round(baseMsrpAmount.value * 0.008).toFixed(2)
//   } else {
//     return Math.round(baseMsrpAmount.value * 0.02).toFixed(2)
//   }
// })

// const transTotal = computed(() => {
//   // Base MSRP * 1.35%
//   // if value is under 50 (any hundred amount) round down,
//   // else round up next dollar amount
//   if (baseMsrpAmount.value == null) return (0).toFixed(2)
//   const value = (baseMsrpAmount.value * 0.0135).toFixed(2)
//   let val = Math.floor(Math.round(Number(value)))
//   const dollarVal = val % 100
//   if (dollarVal > 50) return (val + 1).toFixed(2)
//   return val.toFixed(2)
// })

// const vpbTotal = computed(() => {
//   // Base MSRP * 1.9%
//   if (baseMsrpAmount.value == null) return (0).toFixed(2)
//   return Math.round(baseMsrpAmount.value * 0.019).toFixed(2)
// })
</script>
