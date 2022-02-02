<template>
  <main class="container">
    <div class="row">
      <h1 class="title">PRograms API</h1>
      <div class="col-12">
        <div v-for="type in degreeType" :key="type">
          <nuxt-link :to="`/programs-api/${type}`">{{ type }}</nuxt-link>
        </div>
      </div>
      <div>{{ data }}</div>
    </div>
  </main>
</template>

<script>
export default {
  //fetchOnServer: false,
  data() {
    return {
      currentStep: 1,
      ctaData: {
        text: 'Start your journey',
      },
      degreeType: null,
      data: [],
    }
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get(
      'https://cms.asuonline.asu.edu/lead-submissions-v3.5/programs',
      {
        headers: { Accept: 'application/json' },
      }
    )
    const degreeType = [...new Set(data.map((item) => item.category))].sort(
      (a, b) => {
        return a - b
      }
    )
    return { degreeType, data }
  },
}
</script>

<style></style>
