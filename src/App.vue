<script setup>
import { RouterView } from 'vue-router'
import PageLink from '@/components/PageLink.vue'

import HomeVariantIcon from 'vue-material-design-icons/HomeVariant.vue'
import CalculatorIcon from 'vue-material-design-icons/Calculator.vue'
import InformationVariantCircleIcon from 'vue-material-design-icons/InformationVariantCircle.vue'
</script>

<template>
  <header>
    <nav class="flex justify-between ps-1 pe-1">
        <div class="flex justify-center gap-1">
          <PageLink linkTo="/">
          <HomeVariantIcon />
          </PageLink>
          <PageLink linkTo="/vw-calc">
          <CalculatorIcon />
          </PageLink>
        </div>
        <PageLink linkTo="/about">
          <InformationVariantCircleIcon />
        </PageLink>
    </nav>
  </header>
  <main class="mt-8 p-4">
    <RouterView />
  </main>
</template>
