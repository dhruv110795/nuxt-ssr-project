<template>
  <main>
    <base-header></base-header>
    <nuxt></nuxt>
  </main>
</template>

<script>
import BaseHeaderVue from '~/components/BaseHeader.vue'
export default {
  components: {
    'base-header': BaseHeaderVue,
  },
}
</script>

<style></style>
