
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
      <div>{{ data.length }}</div>
        <nuxt-link to="/programs-api">back to list</nuxt-link>
      <div>{{ data }}</div>
    </div>
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
      'https://cms.asuonline.asu.edu/lead-submissions-v3.5/programs?category='+this.$route.params.id,
      {
        headers: { Accept: 'application/json' },
      }
    )
    this.data = data
  },
}
</script>
