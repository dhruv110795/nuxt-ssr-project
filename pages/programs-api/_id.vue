<template>
  <div>
    <div v-if="$fetchState.pending">
      <h3>Loading</h3>
    </div>
    <div v-if="$fetchState.error">
      <h1>
        {{ $fetchState.error.statusCode }} An error occurred:
        {{ $fetchState.error.message }}
      </h1>
    </div>
    <div v-else>
      <h1>{{ this.$route.params.id }}</h1>
      <div>{{ filteredProgs }}</div>
    </div>
    <nuxt-link to="/programs-api">back to list</nuxt-link>
  </div>
</template>
<script>
export default {
  data() {
    return {
      data: [],
      filteredProgs: [],
    }
  },
  async fetch() {
    const data = await this.$http.$get(
      'https://cms.asuonline.asu.edu/lead-submissions-v3.5/programs',
      {
        headers: { Accept: 'application/json' },
      }
    )
    const filteredProgs = data.filter(
      (progs) => progs.category === this.$route.params.id
    )
    console.log(filteredProgs.length)
    return { filteredProgs, data }
  },
}
</script>
